# Setting Up a Pre-Commit Hook

Set up Pre-Commit Hook Rules to automatically check for sensitive information, such as passwords, API keys, or personal data, before committing code.

## Setup Git Template

1. Clone the template repository:

    ```sh
    git clone https://github.com/bouygues-construction-public/git-hook-rules.git
    ```

2. Configure the template:

    ```sh
    git config --system init.templatedir "C:/Users/son.nguyen/git-template/git-hook-rules"
    ```

Now, you can clone a new project for testing:

```sh
git clone <your-new-project-url>
```

Then, check the `.git/hooks` directory. You will find the `pre-commit` hook file and the `violation-checklist.txt` rule file.

## For exist repositories
For existing repositories on your computer, copy the `pre-commit` hook file and the `violation-checklist.txt` rules file to each repository's `.git/hooks` directory.