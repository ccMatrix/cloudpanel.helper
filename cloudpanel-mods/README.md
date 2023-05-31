# Apply CloudPanel UI mods

## Setup your mod

Create a new folder `/home/clp/htdocs/app_mod/`. Inside keep the same directory structure as CloudPanel uses.

For example if you want to overwrite the file
`/home/clp/htdocs/app/files/templates/Frontend/Dashboard/Partial/information.html.twig` you would create a file
`/home/clp/htdocs/app_mod/files/templates/Frontend/Dashboard/Partial/information.html.twig`.

## Copy the script

Copy the file `clp-install-mod` to `/usr/local/bin/`

## Assign alias

CloudPanel uses the command `clp-update` to install updates. We can overwrite that command with an alias:
Add or create the file `/root/.bash_aliases` with the following contents:

```
alias clp-update='/usr/bin/clp-update && /usr/local/bin/clp-install-mod'
```

Now when you login and run `clp-update` it will first pull any update and afterwards apply the mod and clear the twig prod cache.