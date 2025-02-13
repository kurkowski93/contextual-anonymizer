---
annotations_creators:
- machine-generated
language:
- en
language_creators:
- machine-generated
license: mit
multilinguality:
- monolingual
pretty_name: Contextual Text Anonymizer Dataset
size_categories:
- unknown
source_datasets:
- original
task_categories:
- text2text-generation
- token-classification
task_ids:
- named-entity-recognition
- text-simplification
tags:
- anonymization
- privacy
- gdpr
- synthetic-data
---

# Contextual Text Anonymizer Dataset

## Dataset Description

This dataset contains synthetically generated pairs of texts (original and anonymized) for various document types. The dataset was created for training text anonymization models while preserving context.

### Document Types

The dataset includes examples from the following categories:
- Medical records
- Banking documents
- Business correspondence
- Recruitment documents
- Social media content
- Legal documents
- Educational records
- Insurance documents
- Chat conversations
- Email threads

### Anonymization Tags

The dataset uses the following GDPR-compliant tags:
- [NAME] - Personal names
- [EMAIL] - Email addresses
- [PHONE] - Phone numbers
- [ADDRESS] - Physical addresses
- [PESEL] - Polish national ID numbers
- [NIP] - Polish tax identification numbers
- [DATE] - Dates
- [ACCOUNT] - Bank account numbers

and more...

## Data Structure

Each example in the dataset contains:
- Original text
- Anonymized version of the text
- Used anonymization tags

## Applications

The dataset is designed for:
- Training text anonymization models
- Evaluating anonymization effectiveness
- Research on context preservation in anonymization by LLMs
- Development of privacy protection systems

## Generation Process

The data was generated using GPT models with the following parameters:
- Model: GPT-4o-mini
- Temperature: 0.3 (for consistent and realistic results)
- Batch size: 5 examples
- Diverse templates for each document type

## Limitations

- The dataset contains only synthetic data
- May not cover all edge cases present in real documents
- Focuses mainly on English language contexts

## Ethical Considerations

The dataset was created with privacy protection in mind and does not contain any real personal data. All examples are synthetic.

## Citation

If you use this dataset in your work, please cite:

```
@dataset{contextual_anonymizer_dataset,
  author = {Kurkowski, Michał},
  title = {Contextual Text Anonymizer Dataset},
  year = {2025},
  publisher = {https://github.com/kurkowski93},
  url = {https://huggingface.co/datasets/kurkowski/synthetic-contextual-anonymizer-dataset}
}
``` 