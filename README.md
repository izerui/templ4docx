# templ4docx - Utility library for filling templates in docx files. 
The heart of this library is `apache-poi`

Thanks to `templ4docx` you can read the entire content (as simple String) of docx file, you can find all variables, register variables pattern and you can fill docx template file by your own map of variables.

The recommended way to get started using templ4docx in your project is a dependency management system – the snippet below can be copied and pasted into your build.
```
<dependency>
    <groupId>com.github.izerui</groupId>
    <artifactId>templ4docx</artifactId>
    <version>2.0.0</version>
</dependency>
```

repository
```
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>
```
[Direct link to jar file ](https://oss.sonatype.org/content/groups/public/pl/jsolve/templ4docx/2.0.0/templ4docx-2.0.0.jar)


## Example usage
basic variable
```
Docx docx = new Docx("template.docx");
docx.setVariablePattern(new VariablePattern("#{", "}"));
    
// preparing variables
Variables variables = new Variables();
variables.addTextVariable(new TextVariable("#{firstname}", "Lukasz"));
variables.addTextVariable(new TextVariable("#{lastname}", "Stypka"));
        
// fill template
docx.fillTemplate(variables);
        
// save filled .docx file
docx.save("lstypka.docx");
```

table variable 
```
Docx docx = new Docx(resource.getPath());
Variables var = new Variables();

TableVariable tableVariable = new TableVariable();

List<Variable> nameColumnVariables = new ArrayList<Variable>();
List<Variable> logoColumnVariables = new ArrayList<Variable>();
List<Variable> languagesColumnVariables = new ArrayList<Variable>();

for (Student student : getStudents()) {
    nameColumnVariables.add(new TextVariable("${name}", student.getName()));
    logoColumnVariables.add(new ImageVariable("${logo}", student.getLogoPath(),40,40));

    List<Variable> languages = new ArrayList<Variable>();
    for (String language : student.getLanguages()) {
        languages.add(new TextVariable("${languages}", language));
    }
    languagesColumnVariables.add(new BulletListVariable("${languages}", languages));
}

tableVariable.addVariable(nameColumnVariables);
tableVariable.addVariable(logoColumnVariables);
tableVariable.addVariable(languagesColumnVariables);

var.addTableVariable(tableVariable);
var.addTextVariable(new TextVariable("${title}","测试表"));
var.addTextVariable(new TextVariable("${end}","结束"));
docx.fillTemplate(var);
docx.save("filledTable.docx");
```

More details:

* [Text Variables](http://jsolve.github.io/java/templ4docx-2-0-0-text-variables/) <br />
* [Image Variables](http://jsolve.github.io/java/templ4docx-2-0-0-image-variables/) <br />
* [Bullet List Variables](http://jsolve.github.io/java/templ4docx-2-0-0-table-variables/) <br />
* [Table Variables](http://jsolve.github.io/java/templ4docx-2-0-0-table-variables/) <br />

