# svelte-dnd-action with customDrop

This is an example use of [svelte-dnd-action](https://github.com/isaacHagoel/svelte-dnd-action)'s customDrop function.

Files can be sorted using drag-and-drop (i.e. the usual capability of svelte-dnd-action), but can also be dragged to Favorites, Folders, or Trash.


1. Favorites make a COPY of the file
2. Folders are used to MOVE the file
3. Trash is used to DELETE the file

## Get started

Install the dependencies...

```bash
yarn install
```

...then start [Rollup](https://rollupjs.org):

```bash
yarn dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running.