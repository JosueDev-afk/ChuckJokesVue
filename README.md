# ChuckJokesVue

Minimalist Vue 3 app that renders a list of Chuck Norris jokes using `v-for` and component composition (parent view providing data to a child view).

## Activity Description

The app creates a Vue instance that returns the following `chuck` data and displays it as a stylized list:

```
chuck: [
  { "value": "Chuck Norris can skydive into outer space." },
  { "value": "The chief export of Chuck Norris is pain." },
  { "value": "Chuck Norris doesn't read books. He stares them down until he gets the information he wants." },
  { "value": "Time waits for no man. Unless that man is Chuck Norris." },
  { "value": "If you spell Chuck Norris in Scrabble, you win. Forever." },
]
```

Implementation highlights:
- Parent view (`App.vue`) defines the `chuck` array and passes it to the child view.
- Child view (`ChuckList.vue`) receives `jokes` via props and renders them with `v-for`.
- Clean, minimalist styling using scoped CSS and the base theme variables.

## Screenshots

Include screenshots of:
- The running app showing the jokes list.
- The code structure highlighting `App.vue` and `ChuckList.vue`.

## Project Setup

```sh
pnpm install
```

### Compile and Hot-Reload for Development

```sh
pnpm dev
```

If you prefer npm:

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
pnpm build
```

## GitHub Repository

Create a repository named `ChuckJokesVue` and push the project:

```sh
# Initialize git (if not already)
git init
git add .
git commit -m "feat: initial Chuck Norris jokes list"

# Create repo on GitHub (via web or gh CLI) and add remote
# Using GitHub CLI (optional):
# gh repo create ChuckJokesVue --public --source . --remote origin --push

# Or manually add the remote URL you created on GitHub:
git remote add origin https://github.com/<your-username>/ChuckJokesVue.git
git push -u origin main
```

## Deliverables

- Report document containing project screenshots and the GitHub repository URL.
- GitHub repository with files for a Vue project and minimalist, aesthetic presentation of the data.