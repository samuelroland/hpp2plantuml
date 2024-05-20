# PlantUML generator for C++

This is a fork used by `ctp`, checkout [its repos](https://github.com/samuelroland/ctp) to use this !

**It is far from being perfect, it works for 95% of the time.**

**Changes made to the CLI and core logic**  
To fit my teacher's needs or just making things prettier, I did a few changes to the source code which you can read in details in the recent commits, but here is a quick recap:
1. Remove extra line breaks to avoid having 3 empty lines between elements
1. Show type after element and colon: `void f()` will be `f(): void` and `long long i` will be `i: long long`
1. Suffix const method with `_const`: (`void f() const;` will be `f_const(): void`)
1. **Support free functions list in a PlantUML note !** It includes some template annotation as prefix. (Only for header files)
1. Skip friend references in class because they are not part of the class
1. Do not sort class members so it's easier to read with the same order as in the code
1. Show detected free functions logs and a message when generation is done
1. Do not include aggregation links as we always need to change them but suggest them instead
1. Impacts suggestion: Do not include any link between 2 classes when the related attribute is static

**Known bugs**
1. **Having an attribute with `{}` initialisation will ignore the attribute**: ex. `size_t number{}` will be missing in the diagram but `size_t number` is okay. This is a bug of CppParser.
1. **Free functions detection doesn't work correctly in implementation files** (methods implementations are considered as normal function sometimes becuase). The bug is in CppParser: even when this is a method, the fn['class'] attribute is None because return type is not correctly parsed in some case. **Detection has been disabled in `.cpp` files to avoid having this issue. This might ignore some free functions not present in header files.**

**Disclaimer**: this codebase is old and not necessarly well architectured, I changed it without much consideration on code quality and because I'm not sufficient with Python... It is based on CppParser which is deprecated and has bugs that impact this project (see known bugs above). I didn't update the tests because I can't run them sadly.

**See the original README in [README.rst](README.rst)**


**How to run easily without ctp ?**
This was not documented in main readme so here it is
```sh
python src/hpp2plantuml/hpp2plantuml.py  -i "path/to/cpp/project/**/*.h" -o out.puml
```

Globall install
```sh
pip install .
```