Welcome to our documentation site.
## Contributing
This documentation is for you to use. Please help us keeping it accurate and up to date. To amend content, follow instructions
below.
### Simple edits
All the documentation sits in the `docs/` folder of this repository and is authored leveraging
[markdown](https://en.wikipedia.org/wiki/Markdown) format. The site is then generated with [`mkdocs`](https://www.mkdocs.org/) and
[`mkdocs-material`](https://squidfunk.github.io/mkdocs-material/) theme.
To edit any page, click on the pen icon at the top right of the page. It will take you to the GitLab online editor. You can use
plain markdown and enhance it with all the [features of mkdocs-material](https://squidfunk.github.io/mkdocs-material/reference/).
### Advanced edits
For advanced edits and the ability to preview the site as you make edits, we recommend to edit locally on your PC with an editor like Visual Studio Code.
Instructions:
1. [Install Python](https://www.python.org/downloads/) (select "for my user", and make sure to add python in the path)
2. [Install Visual Studio Code](https://code.visualstudio.com/)
3. [Install GIT](https://git-scm.com/downloads)
4. Fork the repository into your own account to be able to push changes
5. Clone the repository locally
6. Open a terminal
7. Prepare the Python environment
  - Linux
    ```shell
    $ python3 -m venv venv
    $ source venv/bin/activate
    $ pip3 install -r requirements.txt
    ```
    Depending on your specific setup, you might need to slightly change the commands if you work on Windows:
  - Windows
    ```bash
    $ python -m venv venv
    $ source venv/Scripts/activate
    $ pip install -r requirements.txt
    ```
8. Start mkdocs
    ```bash
    $ mkdocs serve
    ```
9. Launch your web browser: `http://127.0.0.1:8000`
    Once you've done this locally once, your `venv/` directory will be stored in your local laptop but not committed to Git because
    it's in the `.gitignore`.  Effectively, mkdocs will remain installed in this Python virtual environment, so coming back to this site to edit locally is as simple as running:
    ```bash
    source venv/bin/activate
    mkdocs serve
    ```
10. Run tests
    GitLab CI will run a number of tests to check for spelling mistakes, markdown syntax and hyperlinks.
    Run those tests locally by issuing the command `make tests`
    ```shell
    make tests
    ```
11. Prepare your GIT merge request:
    ```bash
    $ git checkout -b my-changes
    $ git add .
    $ git commit -m "Docs: add xyz"
    $ git push -u origin my-changes
    ```
12. Issue the merge request so that we can consider your changes
13. Thank you for your help in making documentation better!
