# EduAlexxis's Jailbreak Repo
A Cydia/Sileo repository, hosted at [edualexxis.github.io/jailbreakrepo](https://edualexxis.github.io/jailbreakrepo). Pages are styled with [Bootstrap](http://getbootstrap.com/).

Most data for this repo is stored on XML files and are loaded on the depiction page dynamically. See the guide below on how to set it up. Note that this guide doesn't cover creating .deb files but will briefly cover assiging depictions.

## Setup status

This repo is already personalized and set up for GitHub Pages at `https://edualexxis.github.io/jailbreakrepo`. To finish publishing it:

1. Push this repo to GitHub as `jailbreakrepo` under the `EduAlexxis` account.
2. In the repo's Settings → Pages, enable GitHub Pages for the `main` branch (root folder).
3. Add `https://edualexxis.github.io/jailbreakrepo/` as a repo source in Cydia/Sileo/Zebra.

What's already been customized:
- `Release` — Origin/Label/Description set to this repo's name.
- `index.html` — title, heading, and "Add to Sileo" link point to this repo.
- `repo.xml` — footer links point to this GitHub repo.
- `Packages` / `Packages.bz2` — lists this repo's own packages only.

## Adding your first package to your repo

#### 1. Adding a simple depiction page

Go to the `depictions` folder and create a new folder named after your package's identifier (e.g. `com.yourname.yourtweak`).
Inside it, add 2 files - `info.xml` and `changelog.xml`.
The tags are pretty much self-explanatory.

`info.xml`.
```xml
<package>
    <id>com.yourname.yourtweak</id>
    <name>Your Tweak</name>
    <version>1.0.0-1</version>
    <compatibility>
        <firmware>
            <miniOS>5.0</miniOS>
            <maxiOS>7.0</maxiOS>
            <otherVersions>unsupported</otherVersions>
            <!--
            for otherVersions, you can put either unsupported or unconfirmed
            -->
        </firmware>
    </compatibility>
    <dependencies></dependencies>
    <descriptionlist>
        <description>Describe your tweak here.</description>
    </descriptionlist>
    <screenshots></screenshots>
    <changelog>
        <change>Initial release</change>
    </changelog>
    <links></links>
</package>
```

`changelog.xml`.
```xml
<changelog>
    <changes>
        <version>1.0.0-1</version>
        <change>Initial release</change>
    </changes>
</changelog>
```


#### 2. Link the depiction page your tweak's `control` file

You can add the depictions url at the end of your package's `control` file before compiling it.
The depiction line should look like this:

```text
Depiction: https://edualexxis.github.io/jailbreakrepo/depictions/?p=[idhere]
```

Replace `[idhere]` with your actual package name.

```text
Depiction: https://edualexxis.github.io/jailbreakrepo/depictions/?p=com.yourname.yourtweak
```

#### 3. Rebuilding the `Packages` file

With your updated `control` file, build your tweak.
Store the resulting `.deb.` file into the `/debs/` folder of your repo.
Build your `Packages` file and compress with `bzip2`.

```sh
user:~/ $ cd repo
user:~/repo $ dpkg-scanpackages -m ./debs > Packages
user:~/repo $ bzip2 Packages
```

_Windows users, see [scanpkg](https://github.com/mstg/scanpkg)._

#### 4. Cydia at last!

If you haven't done yet, go ahead and add your repo to Cydia.
You should now be able to install your tweak into your own repo.
