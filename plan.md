# Plan for Local Development Setup of Jekyll Website

This document outlines the steps to set up and run the Jekyll-based website in a local development environment. We will use `rbenv` to manage the Ruby version.

## 1. Prerequisites

Before you begin, make sure you have the following installed on your system:

-   **Homebrew** (for macOS users): A package manager for macOS. If not installed, you can get it from brew.sh. For Linux, use your distribution's package manager (e.g., `apt`, `yum`).
-   **Git**: For version control.
-   **A Code Editor**: Such as Visual Studio Code, Sublime Text, or Atom.

## 2. Install `rbenv` and Ruby

`rbenv` allows you to manage multiple Ruby versions on your machine.

1.  **Install `rbenv` and `ruby-build`:**
    -   On macOS with Homebrew:
        ```bash
        brew install rbenv ruby-build
        ```
    -   For other systems, please follow the official `rbenv` installation guide.

2.  **Initialize `rbenv`:**
    Add the following line to your shell's configuration file (e.g., `~/.zshrc`, `~/.bash_profile`, or `~/.bashrc`):
    ```bash
    eval "$(rbenv init -)"
    ```
    Then, restart your terminal for the changes to take effect.

3.  **Install Ruby:**
    GitHub Pages, which this site is compatible with, currently recommends Ruby 3.1.x. Let's install a recent stable version.

    ```bash
    rbenv install 3.1.4
    ```

4.  **Set the Local Ruby Version:**
    Navigate to your project's root directory (`/home/user/murriel.github.io`) and set the Ruby version for this project:

    ```bash
    cd /home/user/murriel.github.io
    rbenv local 3.1.4
    ```
    This will create a `.ruby-version` file in your project directory.

## 3. Install Project Dependencies

We will use `Bundler` to manage the Ruby gems (dependencies) for the project.

1.  **Create a `Gemfile`:**
    A `Gemfile` is missing from the project. Create a new file named `Gemfile` in the root of your project (`/home/user/murriel.github.io/Gemfile`) with the following content. The `github-pages` gem conveniently includes Jekyll and all other dependencies used by GitHub Pages.

    ```ruby
    source "https://rubygems.org"

    gem "github-pages", group: :jekyll_plugins
    ```

2.  **Install Bundler:**
    Bundler is a gem that manages other gems.

    ```bash
    gem install bundler
    ```

3.  **Install Gems:**
    Now, use Bundler to install all the gems specified in your `Gemfile`.

    ```bash
    bundle install
    ```

## 4. Run the Local Jekyll Server

With all the dependencies installed, you can now serve the website locally.

1.  **Start the Server:**
    Run the following command from your project's root directory:

    ```bash
    bundle exec jekyll serve
    ```

2.  **View Your Site:**
    Jekyll will build your site and start a local web server. You can view your website by opening your web browser and navigating to:

    **http://127.0.0.1:4000/**

    The server will automatically watch for changes to your files and regenerate the site when you save them.

## 5. Troubleshooting

-   **macOS Command Line Tools**: If you encounter errors during gem installation on macOS, you might need to install the Xcode command-line tools:
    ```bash
    xcode-select --install
    ```
-   **Google Maps API Key**: The file `_includes/js.html` contains a Google Maps API key. Please be aware that this key is exposed. For a production site, it's highly recommended to restrict the API key to your domain to prevent unauthorized use.