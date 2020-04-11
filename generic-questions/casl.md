# Handle user permisions with react & CASL

In authenticated frontend apps, we often want to change what’s visible to the user depending on their role. For example, a guest user might be able to see a post, but only a registered user or an admin sees a button to delete that post.

Managing this visibility may become a nightmare for a UI application. You probably have written or seen code like this before:

```jsx
if (user.role === ADMIN || (user.auth && post.author === user.id)) {
  <button onClick={this.deletePost.bind(this)}>Delete</button>;
}
```

This code is spread over the application and usually becomes a big problem when a Product Owner requests to add additional roles in the app. Eventually you need to go through all such ifs and add additional checks.

In this article, I will demonstrate an alternative way to implement permission management by using a neat library which is called CASL. It makes managing active user permissions very simple, and allows you to rewrite the previous example to something like this:

```jsx
if (ability.can('delete', post)) {
  <button onClick={this.deletePost.bind(this}>Delete</button>
}
```

## Defining user permissions

```jsx
import { AbilityBuilder } from "casl";

/**
 * Defines how to detect object's type: https://stalniy.github.io/casl/abilities/2017/07/20/define-abilities.html
 */
function subjectName(item) {
  if (!item || typeof item === "string") {
    return item;
  }

  return item.__type;
}

export default AbilityBuilder.define({ subjectName }, can => {
  can(["read", "create"], "Todo");
  can(["update", "delete"], "Todo", { assignee: "me" });
});
```

The first argument passed to define method is an `options` object. When CASL checks an entity to determine permission, it needs to know the type of entity it’s looking at. The way to do it is to pass `subjectName` property in `options`. In our case, we are looking for custom `__type` property which defines object type (by default, CASL looks for property `modelName` or `name` on object’s `constructor` property).

The second argument is a DSL function which accepts 2 arguments: `can` and `cannot` (we don’t use in `cannot` this example). We define user permissions by calling `can` function. The first argument of can is an action (or an array of actions). Usually it will be a CRUD action but you can specify whatever is suitable for your application (e.g., you can define `can('visit', '/protected/path')` and later check `ability.can('visit, '/protected/path')`). The second argument is object type, in our case `Todo`, for which this rule is applicable.

Pay attention that in the second `can` function call, we pass a third argument which is called conditions. This is used to test if the specified `assignee` value matches an `assignee` property of an object we’ll provide when making the test (e.g., `ability.can('read', todo)`). If we didn’t do this, any todo could be updated or deleted by any user, not just the assignee.

## Checking Permissions in React

At first, you may think that integration will be quite easy: just import created `ability`, add `if`s around some components in `render` function and we are done. That may work but only until you don’t change ability rules.

Why? Because React re-renders a component only in case its state or props are changed. In our case we need to re-render components when `ability` rules are changed, because we will need to update permission rules when a user either logs in or logs out (or logs in under another account).

So, the way to go is to create a custom `Can` component. This component will have two props:

- `run` which accepts action name;
- `on` which accepts subject (subject can be either a string or an object).

And one state property `allowed` which caches the check of `ability.can(this.props.run, this.props.on)`.

If a user has permission to run the specified action on the subject, our component will render passed in children. Eventually we will be able to check permissions like this:

```jsx
<Can run="delete" on={this.props.todo}>
  <button onClick={this.deleteTodo.bind(this}>Delete</button>
</Can>
```

To track permission updates, we can utilize `update` event of Ability instance. We can do this with help of React hooks: `componentWillMount` and `componentWillUnmount`:

```jsx
class Can extends PureComponent {
  //...

  componentWillMount() {
    this.unsubscribeFromAbility = ability.on("update", () => {
      setTimeout(() => this.recheck(), 0);
    });
    this.recheck();
  }

  componentWillUnmount() {
    this.unsubscribeFromAbility();
  }

  //...
}
```

We added `setTimeout` call because CASL emits `update` event before updating permissions. It will be possible to utilize the `updated` event in the 1.1.1 version of CASL.

The only thing which is left is to wrap your UI components in `Can` checks and that’s it.

To play around with your permissions logic, just open Dev Tools and type:

- `ability.update([])` to reset all permissions (i.e., readonly mode);
- `ability.update([{ subject: 'all', actions: 'manage' }])` to get full access to manage everything;
- `ability.rules` to get a list of current abilities;
- for more information about possible options and how to configure `ability` please read in [official documentation](https://stalniy.github.io/casl/).
