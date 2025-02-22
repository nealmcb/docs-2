---
title: Troubleshooting
slug: /streamlit-community-cloud/troubleshooting
---

# Troubleshooting

Sorry to hear you're having issues! Please take a look at some frequently asked questions and issues below. If you cannot find an answer to your issue, please post on our [Community forum](http://discuss.streamlit.io) so that our engineers or community members can help you.

## Table of contents

1. [General help](#general-help)
2. [Deploying apps](#deploying-apps)
3. [Sharing and accessing apps](/streamlit-community-cloud/troubleshooting#sharing-and-accessing-apps)
4. [Data and app security](/streamlit-community-cloud/troubleshooting#data-and-app-security)
<!-- 5. [Billing and administration](/streamlit-community-cloud/troubleshooting#billing-and-administration) -->
5. [GitHub integration](/streamlit-community-cloud/troubleshooting#github-integration)
6. [Limitations and known issues](/streamlit-community-cloud/troubleshooting#limitations-and-known-issues)

## General help

### How can I get help with my app?

If you have any questions, feedback, run into any issues, or need to reach us, you can ask on our [Community forum](https://discuss.streamlit.io/). This is best suited for any questions related to the open source library and Community Cloud - debugging code, deployment, resource limits, etc.

<!-- - Ask on the [forum](https://discuss.streamlit.io) ⬅️ this is best for any question related to the open source library
- Email us at [support@streamlit.io](mailto:support@streamlit.io) ⬅️ this is best for anything related to the app platform - deployment, SSO, etc.

If you want, we are also happy to help lend an eye on your app development. Just shoot us a note if you want to share some code or have our team take a look at your app and give you some tips. -->

## Deploying apps

### My repo isn't showing on the Deploy page

It's possible it just isn't showing up even though it is already there. Try typing it in. If we don't recognize it, you'll see the message below with a link to click and give access.

![Troubleshooting deploy page](/images/streamlit-community-cloud/troubleshooting-deploy-page.png)

If for some reason that doesn't work, please try logging out and back in again to make sure the change took effect. And if that doesn't work - please let us know and we'll get you sorted!

### It won't let me deploy the app

To deploy an app for the first time you must have admin-level access to the repo in GitHub. Please check with your administrator to make sure you have that access. If not, please ask them to deploy for the first time (we need this in order to establish webhooks for continuous integration) and from there you can then push updates to the app.

### I need to set a specific Python version for my app

When deploying an app, under advanced settings, you can choose which version of Python you wish your app to use.

![Streamlit Community Cloud Advanced settings](/images/streamlit-community-cloud/advanced-settings.png)

### How do I store files locally?

If you want to store your data locally as opposed to in a database, you can store the file in your GitHub repository. Streamlit is just python, so you can read the file using:

`pandas.read_csv("data.csv")` or `open("data.csv")`

<Tip>

If you have really big or binary data that you change frequently, and git is feeling slow, you might want to check out [Git Large File Store (LFS)](https://git-lfs.github.com/) as a better way to store large files in GitHub. You don't need to make any changes to your app to start using it. If your GitHub repo uses LFS, it will now _just work_ with Streamlit.

</Tip>

### My app is running into issues while deploying

Check your Cloud logs by clicking on the "Manage app" expander in the bottom right corner of your screen. Often the trouble is due to a dependency not being declared. See here for [more information on dependency management](/streamlit-community-cloud/get-started/deploy-an-app/app-dependencies).

<!-- If that's not the issue, then please send your Streamlit contact the logs and warning you are seeing and we'll help get you sorted! -->

If that's not the issue, then please send the logs and warning you are seeing to our [Community forum](https://discuss.streamlit.io/) and we'll help get you sorted!

### My app is hitting resource limits / my app is running very slowly

If your app is running slowly or you're hitting the 'Argh' page, we first highly recommend going through and implementing the suggestions in the following blog posts to prevent your app from hitting the resource limits and to detect if your Streamlit app leaks memory:

- [Common app problems: Resource limits](https://blog.streamlit.io/common-app-problems-resource-limits/)
- [3 steps to fix app memory leaks](https://blog.streamlit.io/3-steps-to-fix-app-memory-leaks/)

If you're still having issues, click [here](/streamlit-community-cloud/get-started/manage-your-app#app-resources-and-limits) to learn more about resource limits.

### Can I get a custom URL for my app?

Yes! You can find [instructions for setting a custom subdomain here](/knowledge-base/deploy/custom-subdomains).

## Sharing and accessing apps

### I don't have SSO. How do I sign in to Streamlit?

Don't have SSO? No problem! You can sign in to Streamlit with your email address. [Click here](/streamlit-community-cloud/get-started#sign-in-with-email) for step-by-step instructions on how to sign in with email.

<!-- ### How do I add developers to my Streamlit for Teams account?

If you are on the same GitHub repo then you will automatically be added to the same workspace. Just invite them to log in to [share.streamlit.io](http://share.streamlit.io) and we will automatically route them to your workspace once they hook in their GitHub account. -->

### How do I add viewers to my Streamlit apps?

<!-- By default, all apps deployed with Streamlit Community Cloud Teams and Enterprise are private—which means that others in your company won't be able to view them unless you give them explicit permission. To add viewers, [configure single sign-on](/streamlit-community-cloud/get-started/share-your-app/configuring-single-on-sso) with your organization's SSO provider.

If you cannot implement single sign-on, but want to secure your Streamlit app with passwords, read our guide on [authentication without SSO](/knowledge-base/deploy/authentication-without-sso). Note: while this technique adds some level of security, it is **NOT** comparable to proper authentication with an SSO provider. -->

Viewer auth allows you to restrict the viewers of your private app. To access your app, users have to authenticate using an email-based passwordless login or Google OAuth. To learn more about how to share your public and private apps with viewers, click [here](/streamlit-community-cloud/get-started/share-your-app).

### Do viewers need access to the GitHub repo?

Nope! You only need access to the GitHub repo if you want to push changes to the app.

### What will unauthorized/logged out viewers see when they view my app?

A 404 error is displayed to unauthorized viewers to avoid providing any unnecessary information about your app to unintended viewers. Users who satisfy any of the following conditions will see a 404 error when attempting to view your app after you have configured viewer auth:

- User is not logged in with Google SSO.
- User is not included in the [list of viewers](/streamlit-community-cloud/get-started/share-your-app#adding-viewers-from-the-app-dashboard) provided in the app settings.
- User lacks read access to your app's GitHub repo.
<!-- - User has read access to your app's GitHub repo but is not enrolled in Streamlit for Teams beta. -->
- User has read access to your app's GitHub repo but is not enrolled in Community Cloud.

![Four Oh Four](/images/streamlit-community-cloud/404.png)

### I've added someone to the viewer list but they still see a 404 error when attempting to view the app

If a user is still seeing a 404 error after their email address has been added to the viewer list, we recommend that you:

- Check that the user did not log into a different Google account via Single Sign-On (if you have added their work email address to the viewer list, ask the user to check that they are not logged into their personal Google account, and vice versa).
- Check that the user has navigated to the correct URL.
- Check that the user's email address has been entered correctly in the viewer list.
<!-- - Contact [support@streamlit.io](mailto:support@streamlit.io) and we will be happy to help. -->
- Reach out on our [Community forum](https://discuss.streamlit.io/) and we will be happy to help.

## Data and app security

### How will Streamlit secure my data?

Streamlit takes a number of industry best-practice measures to ensure your code, data, and apps are all secure. Read more in our [Trust and Security memo](/streamlit-community-cloud/trust-and-security).

### How do I set up SSO for my organization?

<!-- If you use Google for authentication, you're all set. Otherwise please refer to our [SSO configuration guides](/streamlit-community-cloud/get-started/share-your-app/configuring-single-on-sso) on how to set up with your SSO provider of choice. -->

Community Cloud uses Google OAuth, by default. If you use Google for authentication you're all set.

## Billing and administration

The Community Cloud is a free service. You don't have to worry about setting up billing or being charged.

<!-- ### Are there limits to resources or to users that I can have?

Your workspace is sized to a certain number of users, apps, and resources for those apps. We'll let you know if you're close to your limit and will reach out to discuss if you'd like to move to a larger workspace.

### Where do I set up billing?

Click on "Settings" in the top right corner of your workspace to open the "Workspace settings" menu. Next, click the "Billing and plans" tab to set up billing in Stripe.

<div style={{ marginBottom: '-2em' }}>
  <Image src="/images/streamlit-community-cloud/setup-billing.png" />
</div>

### When will I be charged?

The Starter plan is free forever, but if you have opted for a Teams account then you will have a 14 day free trial for your workspace.

When your trial is near completion, you will receive automated emails reminding you to set up your billing information (if you haven't already) to continue on your Teams plan. To avoid disruption, we recommend that you set up billing well before your trial ends. Once you have set up your billing information, we will only start charging you once your trial ends. Stripe will automatically bill your account every month and send you a confirmation email.

If you choose not to set up billing, you will be downgraded to the Starter plan after your trial ends. -->

## GitHub integration

### Why does Streamlit require additional OAuth scope?

In order to deploy your app, Streamlit requires access to your app's source code in GitHub and also the ability to manage the public keys associated with the repositories. The default GitHub OAuth scopes are sufficient to work with apps in public GitHub repositories. However, in order to work with apps in private GitHub repositories, Streamlit requires the additional `repo` OAuth scope from GitHub. We recognize that this scope provides Streamlit with extra permissions that we do not really need, and which, as people who prize security, we'd rather not even be granted. Alas, we need to work with the APIs we are provided by GitHub.

### After deploying my private-repo app, I received an email from GitHub saying a new public key was added to my repo. Is this expected?

**This is the expected behavior**. When you try to deploy an app that lives in a private repo, Streamlit Community Cloud needs to get access to that repo somehow. For this, we create a read-only [GitHub Deploy Key](https://docs.github.com/en/free-pro-team@latest/developers/overview/managing-deploy-keys#deploy-keys) then access your repo using a public SSH key. When we set this up, GitHub notifies admins of the repo that the key was created as a security measure.

### What happens when a user's permissions change on GitHub?

Once a user is added to a repository on GitHub, it will take at most 15 minutes before they can deploy the app on Cloud. If a user is removed from a repository on GitHub, it will take at most 15 minutes before their permissions to manage the app from that repository are revoked.

## Limitations and known issues

Here are some limitations and known issues that we're actively working to resolve. If you find an issue [please let us know](mailto:support@streamlit.io)!

- When you print something to the Cloud logs, you may need to do a `sys.stdout.flush()` before it shows up.
- Matplotlib [doesn't work well with threads](https://matplotlib.org/3.3.2/faq/howto_faq.html#working-with-threads). So if you're using Matplotlib you should wrap your code with locks as shown in the snippet below. This Matplotlib bug is more prominent when you share your app apps since you're more likely to get more concurrent users then.

  ```python
  from matplotlib.backends.backend_agg import RendererAgg
  _lock = RendererAgg.lock

  with _lock:
    fig.title('This is a figure)')
    fig.plot([1,20,3,40])
    st.pyplot(fig)
  ```

- All apps are hosted in the United States. This is currently not configurable.
