# Getting Setup for Development

To help others with creating and integrating a Java project into their development environment, I have written this guide to set up and clone projects:

1.  Create and set up your project
2.  Integrate with an IDE (IntelliJ IDEA & VS Code/Codium)
3.  Manually compile and run through the command-line

This guide mostly uses the command-line for basic actions like creating directories (folders), files and cloning git repos. These are easily done through graphical interfaces if you so wish to use them. Just make sure you know what you are doing!

>   If you want to know how to use Git and GitHub for this project, check the `README.git.md` file. You don't need to know how to use Git, but you need to at least have it installed to use follow this guide.

###  I've created a supplemental video for this guide [here](https://youtu.be/4UBpOfvAaQw) 

## Creating and Setting Up Your Java Project

Firstly, if you are cloning an existing GitHub repository that was initialized using this guide, you can skip to the Setup section.

>   Setting up your project using an IDE is perfectly valid, but doing it manually is fairly easy and makes you understand what you are doing.

To start a new project, create a new folder to house your new project on your computer:

```
mkdir your_project_name
cd your_project_name
```


### Create `src` For All Source Code

You will write all of your source code here. This includes all `.java` files and subfolder/packages.

```
mkdir src
```

### Create `lib` For All External Libraries/Dependencies

When including external libraries in your source code, make sure the library is in a `.jar` file within the `lib` folder.

<ins>Please avoid copying source code from external libraries into the `src` folder.</ins>

```
mkdir lib
```

### Create the `Main.java` File

This will house the main method for your program. As said before, all `.java` files will be in the `src` folder

>   For Windows (Powershell)
```powershell
New-Item .\src\Main.java
```

>   For Linux/MacOS
```bash
touch src/Main.java
```

### Create the `.gitignore` File

This is to tell Git to ignore files and directories made by IDEs and you when tracking changes. You'll create one at the root folder, which will be your main .gitignore file and one inside the lib folder, to make sure the lib folder is also commited even when it is empty. You do not need to write anything to the .gitignore file in the `lib` folder.

>   For Windows (Powershell)
```powershell
New-Item .gitignore
New-Item lib/.gitignore
```

>   For Linux/MacOS
```bash
touch .gitignore
touch lib/.gitignore
```
####    Write To the 2 `.gitignore` File

Using a text editor like notepad, TextEdit, vim, etc., open the `.gitignore` file and add what you don't want to be tracked. Below is an example to ignore common files created by IDEs and MacOS

```
### IntelliJ IDEA ###
.idea
*.iml
out

### VS Code/Codium ###
.vscode

### MacOS ###
.DS_Store

### Classes Folder ###
bin
```

### Initialize the Git Repo and Push to GitHub

If you don't know how to do so, now is a good time to check out the `README.git.md` Git and GitHub quickstart guide.

### Note When Using an IDE to Setup the Project

It is also perfectly possible to setup your Java project using an IDE like IntelliJ or VS Code/Codium. Just make sure to add the files that are exclusive to your development environment in the `.gitignore` file before you initialize the git repository.

If you accidentally commited files that you didin't want to track in the repo, you can remove them from the repo without deleting them from your computer using:

```
git rm -r --cached <file(s) you want to remove>
```

## Integrate the Project into your IDE 

This is probably the **easiest and fastest** way to start devloping for your project. It will allow your IDE to compile and run your program.

##

### For VS Code/Codium Users

>   **Make sure you have the Project Manager for Java extension installed.**

Clone the repository using Git and create `.vscode/settings.json`:

>   If you already have the repository on your local machine (ie. you followed the setup steps above) all you need to do is create the settings file below.

```
git clone <link to project GitHub repo>
cd <name of repo>
mkdir .vscode
```

>   For Windows (Powershell) Users:

```powershell
New-Item .\.vscode\settings.json
```

>   For Linux/MacOS Users:

```bash
touch .vscode/settings.json
```

####    Add SourcePaths to `settings.json`:

**Open the project folder in  VS Code/Codium** and add the lines below into `settings.json`.

```json
{
    "java.project.sourcePaths": ["src"],
    "java.project.outputPath": "bin",
    "java.project.referencedLibraries": [
        "lib/**/*.jar"
    ]
}
```

VS Code/Codium should then automatically create a folder called `bin` and compile whatever is in the `src` folder.

>   If the folder `bin` already exists for some reason, you need to make sure it is empty before declaring your paths in the `settings.json` file.

##

### For IntelliJ Users

####    If you are opening an existing project you've set up:

1. Run the base IntelliJ IDEA launcher.
2. Select `Open` and select your project directory.
3. If you get a pop-up asking to trust the project, click `Trust Project`.
4. Accept all the defaults that IntelliJ asks for your confirmation.
5. Done

####    If you are cloning from a GitHub repo

1. Run the base IntelliJ IDEA launcher.
2. Under the `Projects` home screen, click on the icon labled "Clone Repository"
3. Paste the link to the project's GitHub repo into the URL box.
4. Click on the `Clone` button at the bottom-right.
5. You may need to authorize IntelliJ to access your GitHub account.
6. If you get a pop-up asking to trust the project, click `Trust Project`.
7. Done

IntelliJ should then automatically configure source, output, and external library paths.

##

####    Note for IntelliJ

I have run into issues where IntelliJ does not set up the project workspace correctly which prevents me from compiling and running my program. I have found that (at least for me) this happens when you mess up the configuration files (`.idea` and `.iml`) for IntelliJ by either deleting them or being corrupted/badly merged in the repo. I've also experienced IntelliJ failing to set up the project if there is no Main method (or any code at at all?) inside the source folder.

When this happend to me, I deleted the entire project and cloned the GitHub repo through IntelliJ again (fresh start). Once I did that, IntelliJ finally used whatever voodoo magic it has to setup the project correctly and I was able to compile and run the program. You just need to make sure there is a main method!

I would be cautious and make sure that there are zero IntelliJ configuration files within the repository.

##

## Manual Setup (Command-Line)

If you want to compile and run your program through the command-line, you can just run `Java <path to java file w/ main method>`. However, with more complex projects, with dependencies and packages, doing so will result in compilation and runtime errors.

>   If you already have the repo setup on your machine, skip the clone.

1. Clone the repository using the `git clone` command and create a `bin` directory:

```
git clone <link to project's GitHub repo>
cd <name of GitHub repo>
mkdir bin
cd bin
```

2. Extract all external libraries to the `bin` directory from `lib`:

> Make sure to replace *path/to/lib* to its real path on your system, and you are running this in the `bin` directory.

```
jar -xf path/to/lib/*.jar
```

>   If you decide to include another external library, make sure to include the `.jar` file into the `lib` directory. You would then, have to repeat step 2 when you do.

### Compiling and Running Main

You need to compile `Main.java` using `javac` with the proper flags before attempting to run it using the `java` command.

> Neglecting to do so will result in a compilation or runtime error.

#### To compile `Main.java` using `javac`

Make sure you are running these command in the root project folder.

```
javac -d bin -sourcepath src -cp bin src/Main.java
```

-   `-d <directory>` Specify where to place generated class files.
-   `-sourcepath <path>` Specify where to find input source files. You want to compile all other classes that the Main method uses.
-   `-cp <path>` Specify where to find user class files and annotation processors. Basically points the compiler where other dependencies/libraries that the Main method includes.

#### To Run `Main` Using `java`

Simply run:

```
java -cp bin Main <args>
```

##  Dev Note

While working on your project, Java treats sub-folders within `src` as packages. If you create a class file within that sub-folder, you will need to declare `package <name of sub-folder>` for that class.

Also, classes in that sub-folder will not be able to access methods that you have created in other classes if they are just in the `src` folder. However, they will be able to access them if that method/class is within another or the same package.

Watch the supplumental video for an example.