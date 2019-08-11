
#  First Github pages by travis

- Read here : https://bookdown.org/yihui/bookdown/github.html
- Create a branch named gh-pages and clean up everything

git checkout --orphan gh-pages
git rm -rf .

touch .nojekyll
git add .nojekyll

git commit -m"Initial commit"
git push origin gh-pages

- Create a personal access token for your account on GitHub (make sure to enable the “repo” scope so that using this token will enable writing to your GitHub repos) : http://bit.ly/2cEBYWB

- Create an environment variable GITHUB_PAT with the value of the token

- Create a .travis.yml file with :

# configure your name and email if you have not done so
git config --global user.email "you@example.com"
git config --global user.name "Your Name"

# clone the repository to the book-output directory
git clone -b gh-pages https://${GITHUB_PAT}@github.com/${TRAVIS_REPO_SLUG}.git book-output
cp -r src./* ./book-output
cd book-output
Rscript -e "rmarkdown::render('index.Rmd')"
git add --all -f ./*
git commit --allow-empty -m"Update the book"
git push -q origin gh-pages

