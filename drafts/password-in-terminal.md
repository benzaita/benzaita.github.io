# How to stop typing your password in your terminal on MacOS?

When working from the terminal you sometimes need to provide your password, and typing it in clear text is a bad habit. This post shows how to fetch it from the MacOS KeyChain instead.

## Why is it bad to type your password in the terminal?

Typing your password in the terminal is discouraged because:

1. It is stored in the terminal history in clear text.
1. If you share your screen with someone while typing, they can see it too.
1. It's a repetative task and therefore error prone and annoying.

## Adding your password to the MacOS Keychain

First you need to add that password to the MacOS KeyChain. Open the KeyChain Access application and create a new password item (File > New Password Item...). As an example, we will add a password for "https://example.com". Under "Keychain Item Name" type `https://example.com` (note the `https://`), and under "Account Name" type your user name (e.g. "alice"). Fill in the password and save the item.

## How to fetch the password in the terminal?

We are going to use the `security` command line tool which is provided with MacOS. Let's assume you need to provide the password as an environment variable called `FOO_PASSWORD`, use this:

```bash
export FOO_PASSWORD=$(security find-internet-password -a alice -s example.com -w)
```

## Prompting for the password

Sometimes you might prefer to be required to actually type your password every time. For example, when you run a command to destroy a resource you might actually want to be prompted, to make sure you don't run the command by mistake. In that case, you can use the `read` command. For example, in Bash:

```bash
read -se FOO_PASSWORD
```

You will first be prompted to enter your password (which will be hidden) and then it will be exported to the environment variable `FOO_PASSWORD`.
