# curve-docs
[reStructuredText](https://www.writethedocs.org/guide/writing/reStructuredText/) documentation for [curve.readthedocs.io](https://curve.readthedocs.io/).

## Contributing

Contributions to documentation are always welcome! Feel free to open a pull request of any size.

We adhere to the following guidelines within our documentation. Reviewing them will help ensure a quick and painless code review if you are making a significant contribution.

### Writing Style
We use imperative, present tense to describe APIs: “return” not “returns”. One way to test if we have it right is to complete the following sentence:

    “If we call this API it will: ...”

For narrative style documentation, we prefer the use of first-person “we” form over second-person “you” form.

Additionally, we recommend the following best practices when writing documentation:

* Use terms consistently.
* Avoid ambiguous pronouns.
* Eliminate unneeded words.
* Establish key points at the start of a document.
* Focus each paragraph on a single topic.
* Focus each sentence on a single idea.
* Use a numbered list when order is important and a bulleted list when order is irrelevant.
* Introduce lists and tables appropriately.

Google’s [technical writing courses](https://developers.google.com/tech-writing) are a valuable resource. We recommend reviewing them before any significant documentation work.

### API Directives

* All API documentation must use standard [Python directives](https://www.sphinx-doc.org/en/master/usage/restructuredtext/domains.html#the-python-domain).
* Where possible, references to syntax should use appropriate [Python roles](https://www.sphinx-doc.org/en/master/usage/restructuredtext/domains.html#cross-referencing-syntax).
* External references may use [intersphinx roles](https://www.sphinx-doc.org/en/master/usage/extensions/intersphinx.html).

### Headers
Each documentation section must begin with a [label](https://www.sphinx-doc.org/en/stable/usage/restructuredtext/roles.html#cross-referencing-arbitrary-locations) of the same name as the filename for that section. For example, if the filename for a section is `style-guide.rst`, the RST opens with a label `_style-guide`.

Section headers should use the following sequence, from top to bottom: `#`, `=`, `-`, `*`, `^`.

## License

This project is licensed under the [MIT](LICENSE) license.
