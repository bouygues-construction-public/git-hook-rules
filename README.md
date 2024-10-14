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

Then, check the `.git` directory. You will find the `hooks/pre-commit` file and `rules`, `ssl` folders.

## For existing repositories
For existing repositories on your computer, copy folders `hooks`, `rules`, `ssl` to each repository's `.git` directory.

## How it works
It will detect sensitive information using the rule patterns in the `violation-checklist.txt` file when the commit action is performed

Below is an example, these files contain sensitive information:

```sh
# application-example.yml

version: 0.1

jobs:
  build:
    azure:
      database:
        url: jdbc:postgres://localhost/sampledb?username=user;password=example_password
      ftp:
        username: ftpuser
        password: ftppass
      oauth2:
        client-id: 6779ef20e75817b79602
        secret: 269d98e4922fb3895e9ae2108cbb5064
```

```sh
# example.php

<?php

$databases['default']['default'] = array (
    'database' => 'drupal',
    'username' => 'root',
    'password' => 'example-password',
    'prefix' => '',
    'host' => 'localhost',
    'port' => '3306',
    'namespace' => 'Drupal\\Core\\Database\\Driver\\mysql',
    'driver' => 'mysql',
  );

  define('DB_HOST', 'localhost');
  define('DB_USERNAME', 'root');
  define('DB_PASSWORD', 'example-password');
  
```

```sh
# example.java

String token = "ZYDPLLBWSK3MVQJSIYHB1OR2JXCY0X2C5UJ2QAR2MAAIT5Q";

String urlString = "https://example.com/?token=" + token;
URL url = new URL(urlString);
URLConnection conn = url.openConnection();
InputStream is = conn.getInputStream();
```

When you commit:

```sh
PS C:\Users\son.nguyen\WORKSTATION\RnD\git-hook-rules> git commit -m "test commit"
```

The result will notify you of any code violations and abort the commit.
```sh
There are some code snippets that violate data security rules:


File: application-example.yml

        password: ftppass
        secret: 269d98e4922fb3895e9ae2108cbb5064
        url: jdbc:postgres://localhost/sampledb?username=user;password=example_password

File: example.php

  define('DB_PASSWORD', 'example-password');
  'password' => 'example-password',


...and the warning code snippets:


File: example.java

String token = "ZYDPLLBWSK3MVQJSIYHB1OR2JXCY0X2C5UJ2QAR2MAAIT5Q";
```

We need to add more rule patterns that can cover more cases,

Thank you!
