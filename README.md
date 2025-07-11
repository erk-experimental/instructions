# Working in Amazon Web Services (AWS)

If you choose to run your project on AWS, you'll want to add me as an authorized user to your AWS account. This lets me work on the project under your account, without requiring you to give me your account's login info.

### Follow these steps

First, [create a free-tier AWS account](https://aws.amazon.com/free) and log in.

### Create IAM Role

1. In the AWS console, type `IAM` in the search bar on the top left
2. Click the `IAM` result (should be under `Services`)
3. In the left navbar, under `Access management`, click `Roles`
4. Click the orange `Create role` button on the right
5. Under `Trusted entity type`, choose `AWS account`
6. Under `An AWS account`, check the `Another AWS account` radio button. Enter `992382521243` into the `Account ID` field (this is my personal AWS account)
7. Click `Next`, then add the policy `AdministratorAccess` by typing it into the search bar and checking the box. _This gives me permissions to work with the various AWS services needed to build your project_

8. Click `Next`, then give the role a name. This can be anything you want.
9. Click `Create role`

### Update role settings

1. After creating the role, you should be taken back to the `Roles` page and see the new role in the list
2. Click the new role to open up its page
3. To the right of that, click `Edit`, set `Maximum session duration` to 8 hours, and save. This lets me work without having to constantly log back in.

### IMPORTANT: Send me your role details

On that same role page, look for the `Summary` panel. Send me the `ARN` as well as the URL under `Link to switch roles in console`.

# GitHub hosting and domain

We may decide to use GitHub Pages to host your website. The URL will look like:

```
<github-username>.github.io
```

If you want to use your own custom domain, you can purchase/manage it from any service provider (GoDaddy, Namecheap, etc).

### Set up Git

1. Create a new [GitHub](https://github.com/) account (or use an existing one)
2. Download and install [GitHub Desktop](https://github.com/apps/desktop)

   a. Assuming you're on Mac, unzip the downloaded file and drag the `GitHub Desktop` application to the `Applications` folder

3. Run GitHub Desktop and sign in
4. Use default options to Configure Git

### Download the project

1. In a browser, open the repository URL I sent you (should be in the format `https://github.com/erk-experimental/<repo-name>.git`)
2. Click the green `Code` button, then `Download Zip`
3. Unzip the file and move the folder to anywhere on your computer

### Upload to your own repository

1. In GitHub Desktop, click `add existing repository from local drive`
2. For `local path`, choose the folder you just downloaded
3. Click `add repository`. _There will be an error._
4. In the error message, click `create a repository`
5. The repository name is important, you _must_ set it to:

```
<your-github-username>.github.io
```

For example, if your github username is `good-name`, the repository name must be `good-name.github.io`.

6. Leave all options at their defaults, and create repository
7. At the top, click `Publish repository`
8. Uncheck "keep this code private" (it must be public for GitHub Pages to work)
9. Publish it

Now if you open up [GitHub](https://github.com/) and login, you should be able to see the new repository.

### Hosting on GitHub Pages

1. Open your new repository on GitHub in the browser
2. At the top of the page, open the `Actions` tab
3. There should be a workflow called "Initial commit". If it's still in progress, wait for it to finish
4. Once it's done, open the `Settings` tab
5. In the left sidebar, click on `Pages`
6. Under `Branch`, click the dropdown. There should be an option called `gh-pages`. Click that, then click `save`
7. Wait for a bit as GitHub spins up the website. You'll know it's ready when a message appears saying "Your site is live at..." (you might have to refresh the page to see this)
8. **IMPORTANT**: The URL it gives you should be `http://<your-github-username>.github.io/`. If you see a URL with more text appended after the `github.io/`, you likely didn't name your repository correctly. Rename the repository and make sure to follow the format detailed in the section above.
9. All done! Congrats!

### Setting up your custom domain

#### Add custom domain to GitHub Pages

1. In GitHub, open up your repository and go to `Settings > Pages`
2. Under `custom domain`, enter your custom domain (without the `www` or `https`) and click `save`
3. Check the box for `enforce HTTPS`
4. [Verify your domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages) - this is optional but strongly encouraged because it protects your domain from being taken over by others

#### Add CNAME to your repository:

1. In GitHub, open up your repository
2. Click the `Add file` button (it's next to the green `Code` button)
3. Click `Create new file`
4. Name the file `CNAME`
5. For file contents, enter your custom domain (e.g. `example.com`)
6. Click `Commit changes`, then `Commit changes` again in the popup

#### In your domain service provider

1. Open your domain and find its "settings" or "manage" page
2. If there are any existing A records or CNAMEs, delete them (feel free to save their values first just in case)
3. Create four new A records according to this table (these are GitHub's special IP addresses):

| Type | Name (Host) | Value           | TTL     |
| ---- | ----------- | --------------- | ------- |
| A    | @           | 185.199.108.153 | Default |
| A    | @           | 185.199.109.153 | Default |
| A    | @           | 185.199.110.153 | Default |
| A    | @           | 185.199.111.153 | Default |

4. Create a CNAME record:

   a. Name: `www`

   b. Value: The URL given to you by GitHub Pages (e.g. `<username>.github.io`)

   c. TTL: `Default`

Finally, wait up to 24 hours for changes to propagate, and your custom domain should be working!
