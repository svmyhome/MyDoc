# Create Class, Jar files and Run Jar file

## 1. Create Class file

If you don't have pakages and You want to compile file in the same directory You must run: `javac test/javaMain.java`

If you have packages you must compile files same structure packages. You must run: `javac -d ../../../target/classes/ test/javaMain.java`

---

## 2. Create Jar File



#### ***2.1. Without a package***

You need create the file `manifest.txt` include string `Main-Class: NameMaineClass + Enter`:

for Example: `Main-Class: javaMain + Enter`

run: `jar -cvmf manifest.txt name.jar TruckMain.class`

#### ***2.2. With a package***

You need create the file `manifest.txt` include string `Main-Class: NamePackage + NameMaineClass + Enter`:

for example: `Main-Class: test.javaMain + Enter`

run: `jar -cvmf ./test/manifest.txt name.jar test`

---

## 3. Run Jar File

run: `java -jar name.jar`
