# AI Evaluation Metrics Spike

Status: Completed

## Need
Defra hosts a wealth of documents in varying legacy formats including micro-fiche. A solution for reliably digitising these documents is required.

## Hypothesis

Defra's documents can be accuractly and efficiencly digitised using AI or a simpler, dedicated open-source tool.

## What we aim to discover
- Whether AIs can be used to perform OCR on Defra's document
- Whether VLMs can be used to perform OCR
- Which types of documents can be processed
- How the performance of AIs compare to dedicated tools in this task
- How the AIs should be tuned to best peform this task
- How dedicated tools should be tuned to best peform this task.

## Assumptions
- The reference text in the public datasets for validating OCR is an accurate reflection of the image text
- The types of documents included in the public dataset are representative of the types of documents that Defra want to process

## Outcomes
We used a public dataset of images of text along with the associated annotations to validate the ability of AI (Claude) and a dedicated tool (Tesseract) to peform OCR on four different document types - printed documents, handwritten documents, forms and invoices.  We used documents taken from Defra Sharepoint to validate the same function on Defra documents.

### Key Findings
- The performance of AI in performing OCR on printed documents is comparable to dedicated tools.
- AI outperforms tesseract when doing OCR on hand-writing.  However other tools dedicated to OCR of hand-writing are available.
- Tesseract should be used in auto mode when processing entire pages and line mode when processing individual bounding boxes.
- AIs have a propensity to hallucinate entire sentences which are not included in the source image.  This is potentially very dangerous.
- Different tools perform better on different document types.  A document classifier e.g. using machine-vision should perhaps be used to triage documents to determine the appropriate tool.

## Shortcomings
- We have failed to track down any real-world examples of the types of documents Defra want to process
- One user raised the requirement to OCR river hydrology data stored on micro-fiche, however we cannot seem to track down this user or any micro-fiche data
- Some of the annotations in the public dataset we used were not an accurate representation of the text contained in the source image
- We failed to get VLMs to work on our local machines.  A GPU cluster is required.
