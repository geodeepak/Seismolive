# ObsPy Affiliated Project Guidelines

If you are a developer, or prospective developer, of a seismology package which uses ObsPy we highly recommend you adhere to the following guidelines. Doing so will help ensure your project is maintainable, attractive to potential contributors, and interoperable with other ObsPy-based codes. We also offer some suggestions that you may find useful.

## Guidelines

1. Write your code in a way that is readable and understandable by others. Adhere to [pep8](https://www.python.org/dev/peps/pep-0008/) and the [ObsPy coding style guide](http://docs.obspy.org/coding_style.html), deviating only slightly when there is good reason to do so. Using an automated linter/formatter like [black](https://black.readthedocs.io/en/stable/) or [flake8](http://flake8.pycqa.org/en/latest/) makes this easy.

2. Use classes and functions from ObsPy wherever appropriate. For example, the obspy `Stream`, `Catalog`, and `Inventory` objects should always be valid inputs for functions that require waveform, event, or station data, respectively. This does not mean that other data formats cannot also be supported, but supporting ObsPy data structures is essential for achieving interoperability between seismology packages. 

3. Create documentation that adequately explains the purpose of your package and how to use it. Effective documentation will give the reader a brief explanation of what the software does and demonstrates some simple examples very early on. Additionally, user-facing classes and functions should all have docstrings. 

4. Include an automated test suite that covers your code’s intended functionality as well as possible. Use an existing python testing frameworks like [pytest](https://docs.pytest.org/en/latest/) or [unittest](https://docs.python.org/3/library/unittest.html). 

5. Write code compatible with Python 3. Python 2 compatibility is optional but not advisable for new codes since [many scientific libraries will soon drop Python 2 support](https://python3statement.org/).

6. Be open to contributions from others. Put your code on a hosted collaborative development service like GitHub and apply a standard [open-source license](https://choosealicense.com/) to your project.

## Suggestions

1. Make an effort to connect with the ObsPy developer community. We are a friendly fun-loving group (especially Tobias) and happy to help if you need advice or someone to bounce ideas off. The best place to find us is on [gitter](https://gitter.im/obspy/obspy).

2. Write out a “quickstart” section of your documentation before writing any code, and revisit it often. This will help you keep a user-friendly interface a primary goal during the development cycle.

3. Follow a Test Driven Development ([TDD](https://medium.freecodecamp.org/learning-to-test-with-python-997ace2d8abe)) paradigm which will help you design modular, testable code. However, try to write tests that will not make it difficult to refactor your code later on. Understand that software testing is an art and it will take some time to master.
