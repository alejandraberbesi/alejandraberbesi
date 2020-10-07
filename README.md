### Hi there 👋

<!--
**alejandraberbesi/alejandraberbesi** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->


on:
  schedule:
    - cron: '0 */12 * * *' # every 12 hours
  push:
    branches:
      - master
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
      with:
        fetch-depth: 0
    - name: Generate README.md
      uses: teoxoy/profile-readme-stats@v1
      with:
        token: ${{ secrets.USER_TOKEN }}
    - name: Update README.md
      run: |
        if [[ "$(git status --porcelain)" != "" ]]; then
        git config user.name github-actions[bot]
        git config user.email 41898282+github-actions[bot]@users.noreply.github.com
        git add .
        git commit -m "Update README"
        git push
        fi
