# Chanelle Mosquera's Portfolio

This repository contains the source code for Chanelle Mosquera's personal portfolio website, built with Jekyll.

## Installation and Setup

### Prerequisites
- **Ruby**: Version 3.4.4 or later
- **Jekyll**: Version 4.0.1 or later
- **Bundler**: Version 2.6.9 or later

### Steps to Install and Run

1. **Install Ruby**:
   - If you don't have Ruby installed, you can install it using Homebrew:
     ```sh
     brew install ruby
     ```
   - Add Ruby to your PATH by adding the following line to your `~/.zshrc` file:
     ```sh
     export PATH="/opt/homebrew/opt/ruby/bin:$PATH"
     ```
   - Reload your shell configuration:
     ```sh
     source ~/.zshrc
     ```

2. **Install Jekyll and Bundler**:
   - Install Jekyll and Bundler using RubyGems:
     ```sh
     gem install jekyll bundler
     ```

3. **Clone the Repository**:
   - Clone this repository to your local machine:
     ```sh
     git clone https://github.com/yourusername/chmosquera.github.io.git
     cd chmosquera.github.io
     ```

4. **Install Dependencies**:
   - Install the required gems:
     ```sh
     bundle install
     ```

5. **Run the Site Locally**:
   - Start the Jekyll server:
     ```sh
     bundle exec jekyll serve
     ```
   - Open your browser and go to `http://127.0.0.1:4000/` to view the site.

## Additional Notes
- Ensure that your `Gemfile` includes the necessary gems, such as `csv`, `base64`, and `bigdecimal`, as they are required for the site to run properly.
- If you encounter any issues, make sure to check the console output for error messages and ensure that all dependencies are correctly installed.

My personal website uses the [Jekyll Garden theme](https://github.com/Jekyll-Garden/jekyll-garden.github.io).