---
title: Document Generator
parent: Cloud Client Architecture
---
# Document Generator

You are building an application following the Multimodal Architecture, but you need to communicate with people that (for various reasons) will only accept, or desire documents in a standard form (such as PDF, or Microsoft Office).

**How do you integrate printed or digital documents into a user interaction scenario?**

Even well into the age of the web, as we cross from Web 2.0 into the first glimmerings of Web 3.0, there are still plenty of opportunities to interact with users through that 500+ year precursor to the Web, the printed page.  Documents, whether printed or in simple digital forms like Word or PDF, are still at the heart of many business processes.  This is particularly true when the document is a form that must be filled out to comply with a regulatory procedure, or when this is part of a well-known process such as an RFP (Request for Proposal) response.  

The problem is that many of the simplest mechanisms for attempting to comply with these processes is often unsatisfactory.  For instance, it is possible to print a Web page to PDF, but the result is often difficult to follow, as column widths, diagram sizing and page breaks do not match between the web and the printed page, and thus are usually not well formatted for off-line reading.  If a document must follow a complex format, such as an RFP response or a government form, then the simple printing approach will not work.  The application developers would spend more time formatting their Web site to conform with the output format than they would developing the site functionality itself.  What is needed is a way to separate the document generation function from the other functions of the application.  This begins by realizing that documents are their own user interaction approach, and thus requires its own unique Interaction Model.

Therefore,

**Build a Document Generator that constructs the document on the fly, using similar approaches to the template construction approaches used by Web Applications.**

A Document Generator will often work with a Document Transmission API that sends the document to the user.  This could be an Email API, an API to a file sharing system such as Microsoft SharePoint, or even something as simple as SFTP.  Likewise, a Document Generator will require a set of libraries and services that perform the Document Building function.  An example of this kind of architecture is shown below in Figure 15: Document Generator Architecture:
 
Figure 15: Document Generator Architecture

There are many libraries, both commercial and open source, that enable document building.  One particularly good example for building documents that follow the Microsoft Office formats (for Word, Excel, etc.) is the venerable Apache POI project.  This project (which is built by open-source developers sharing a particularly biting sense of humor) allows you to create documents using the HWPF (Horrible Word Processor Format) or HSSF (Horrible SpreadSheet Format) and even to embed within them drawings created using the DDF (Dreadful Drawing Format).  (It should be noted that these are the names for the older .doc and .xls formats – the names for the newer XML based formats are less derogatory).  Likewise, it is possible to start with template Word files, Powerpoint and Excel files and fill in missing bits using the POI libraries.

Another example for building documents in the Adobe PDF format is the open source PDFKit library for Node.js.  This library allows you to again create complex, multi-part, multipage documents that contain both drawings (rendered in the document) and text, along with formatting.  The results can be transmitted, saved or printed directly. 

* * *

Document Generators are often combined with other digital-native user interaction formats.  For instance, a Web Application or Single Page Application may allow the user to save a nicely formatted Word or PDF document that meets unique presentation requirements.
