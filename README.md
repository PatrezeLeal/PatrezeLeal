Olá! Eu sou o Patreze Leal👋
- 
- 🌱 eu estou estudando programação em java,figma,mysql.
- 💬 contate-me atraves do email patrezeleal@gmail.com
- 😄 Pronomes: ele / dele

##

<div align="center">
  <a href="https://github.com/"PatrezeLeal>
  <img height="150em" src="https://github-readme-stats.vercel.app/api?username=PatrezeLeal&show_icons=true&theme=moltack&include_all_commits=true&count_private=true"/>
  <img height="150em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=PatrezeLeal&layout=compact&langs_count=7&theme=moltack"/>
</div>

  ##
  
  <div>
  
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/figma/figma-original.svg" width="30" height="40"/>
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original-wordmark.svg" width="40" height="40"/>
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original-wordmark.svg" width="40" height="40"/>
  
</div>

# GitHub Action for generating a contribution graph with a snake eating your contributions.

name: Generate Snake

# Controls when the action will run. This action runs every 6 hours.

on:
  schedule:
      # every 6 hours
    - cron: "0 */6 * * *"

# This command allows us to run the Action automatically from the Actions tab.
  workflow_dispatch:

# The sequence of runs in this workflow:
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:

    # Checks repo under $GITHUB_WORKSHOP, so your job can access it
      - uses: actions/checkout@v2

    # Generates the snake  
      - uses: Platane/snk@master
        id: snake-gif
        with:
          github_user_name: patrezeleal
          # these next 2 lines generate the files on a branch called "output". This keeps the main branch from cluttering up.
          gif_out_path: dist/github-contribution-grid-snake.gif
          svg_out_path: dist/github-contribution-grid-snake.svg

     # show the status of the build. Makes it easier for debugging (if there's any issues).
      - run: git status

      # Push the changes
      - name: Push changes
        uses: ad-m/github-push-action@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          branch: master
          force: true

      - uses: crazy-max/ghaction-github-pages@v2.1.3
        with:
          # the output branch we mentioned above
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
