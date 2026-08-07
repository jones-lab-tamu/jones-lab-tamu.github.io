source 'https://rubygems.org'

# GitHub Pages builds this site with its own pinned gem set, currently Jekyll 3.x.
# Depending on `github-pages` keeps local builds identical to what deploys, so a
# template change that works locally cannot fail in CI on a version difference.
# Pinned deliberately: left unpinned, Bundler backtracks to a decade-old release
# to satisfy the script gems below. 232 is the version GitHub Pages runs today.
# To re-sync after GitHub bumps their gem set, raise this number and re-bundle.
gem 'github-pages', '232', group: :jekyll_plugins

# Required for `jekyll serve` on Ruby 3+.
gem 'webrick'

# Used only by the standalone maintenance scripts in _scripts/, not by the site build.
gem 'down'
gem 'execjs'
gem 'netrc'
gem 'octokit'
