## Sejam bem-vindos ao meu github! 👨🏾‍💻

* ### 📊 Algumas informações sobre minhas atividades:
<div>
  <img height="180em" src="https://github-readme-stats.vercel.app/api?username=vicentiin&theme=tokyonight&show_icons=true&hide_border=false&count_private=true" />
  <img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=vicentiin&theme=tokyonight&show_icons=true&hide_border=false&layout=compact" />
</div>

* ### 🌟 Onde eu brilho. Meus principais domínios:
<div style="display: inline_block">
  <img width="50" height="50" align="center" alt="python" src="https://devicon-website.vercel.app/api/python/original.svg" />
  <img width="50" height="50" align="center" alt="django" src="https://devicon-website.vercel.app/api/django/plain-wordmark.svg?color=%23FFFFFF" /> |
  <img width="50" height="50" align="center" alt="html" src="https://devicon-website.vercel.app/api/html5/original.svg" />
  <img width="50" height="50" align="center" alt="css" src="https://devicon-website.vercel.app/api/css3/original.svg" />
  <img width="50" height="50" align="center" alt="js" src="https://devicon-website.vercel.app/api/javascript/original.svg" /> |
  <img width="50" height="50" align="center" alt="reactjs" src="https://devicon-website.vercel.app/api/react/original.svg" />
  <img width="50" height="50" align="center" alt="tailwindcss" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/tailwindcss/tailwindcss-original-wordmark.svg" /> |
  <img width="50" height="50" align="center" alt="java" src="https://devicon-website.vercel.app/api/java/original.svg" />
  <img width="50" height="50" align="center" alt="delphi" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/delphi/delphi-original.svg" />
  <img width="50" height="50" align="center" alt="sql" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/azuresqldatabase/azuresqldatabase-original.svg" />
</div>

##

* ### 🔗 Contato e Redes:
<div style="display: inline_block">
  <a href="mailto:vicentemirandaoffice@gmail.com">
    <img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white" />
  </a>

  <a href="https://www.linkedin.com/in/carlosfilipevicentemiranda/">
    <img src="https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white" />
  </a>
</div>


name: generate animation

on:
  # run automatically every 24 hours
  schedule:
    - cron: "0 */24 * * *" 
  
  # allows to manually run the job at any time
  workflow_dispatch:
  
  # run on every push on the master branch
  push:
    branches:
    - master
    



jobs:
  generate:
    permissions: 
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5
    
  steps:
    # generates a snake game from a github user (<github_user_name>) contributions graph, output a svg animation at <svg_out_path>
    - name: generate github-contribution-grid-snake.svg
      uses: Platane/snk/svg-only@v3
      with:
        github_user_name: ${{ github.repository_owner }}
        outputs: |
          dist/github-contribution-grid-snake.svg
          dist/github-contribution-grid-snake-dark.svg?palette=github-dark
          
          
  # push the content of <build_dir> to a branch
  # the content will be available at https://raw.githubusercontent.com/<github_user>/<repository>/<target_branch>/<file> , or as github page
  - name: push github-contribution-grid-snake.svg to the output branch
    uses: crazy-max/ghaction-github-pages@v3.1.0
    with:
      target_branch: output
      build_dir: dist
    env:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
