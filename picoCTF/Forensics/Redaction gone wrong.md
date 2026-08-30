# Redaction gone wrong

In this challenge, we are presented with a PDF file that contains redacted information.

At first, the black boxes make it look like the text has been properly hidden, but I wanted to check if the actual text was still inside the PDF.

Instead of opening it and trying to read around the redactions, I just extracted all of the text using:

```
pdftotext file.pdf flag.txt
```

This basically takes whatever text is stored inside the PDF and puts it into a normal text file.

After that, I just did:

```
cat flag.txt
```

and we can immediately see that the redacted text is still there, including the flag.

So the redaction was only visual. The black boxes were placed over the text, but the original text itself was never actually removed from the PDF.
