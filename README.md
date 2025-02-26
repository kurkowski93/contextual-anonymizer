# Contextual Text Anonymizer

A comprehensive pipeline for training and deploying text anonymization models with contextual understanding. This project aims to create a robust system for identifying and anonymizing sensitive information in various types of documents while preserving the context and readability of the text.

## Project Structure

1. **Data Generation** (`notebooks/synthetic_data.ipynb`)
   - Generates synthetic training data using GPT models
   - Creates pairs of original and anonymized text
   - Supports multiple document types (medical, banking, business, etc.)
   - Maintains consistent anonymization tags with numerical suffixes

2. **Training Pipeline** (`notebooks/model_training_pipeline.ipynb`)
   - Uses FLAN-T5-small as the base model
   - Fine-tuning process on synthetic data
   - Complete training pipeline including:
     - Data preprocessing
     - Model and tokenizer configuration
     - Training process with metrics monitoring
     - Comprehensive model evaluation with privacy-focused metrics
     - Visualization of performance results
     - Practical inference examples

## Model Training

### Base Model
- **Model**: google/flan-t5-small
- **Architecture**: T5 (Text-to-Text Transfer Transformer)
- **Advantages**:
  - Efficient model size
  - Strong text-to-text capabilities
  - Pre-trained on various tasks

### Training Process
1. **Data Preprocessing**:
   - Adding task-specific prompts
   - Tokenization of inputs and targets
   - Attention mask generation

2. **Training Configuration**:
   - Using Hugging Face Trainer API
   - Hyperparameter optimization
   - Learning process monitoring
   - Checkpoint saving

3. **Evaluation**:
   - **Entity-level metrics**: Precision, Recall, F1 for correctly anonymized data
   - **Text similarity metrics**: BLEU and ROUGE-L to measure text structure preservation
   - **Data privacy metrics**: Detecting and quantifying sensitive information leaks
   - **Visualization**: Charts and summary statistics for model performance analysis


## Dataset

The project includes a synthetic dataset available on Hugging Face Hub: [kurkowski/synthetic-contextual-anonymizer-dataset](https://huggingface.co/datasets/kurkowski/synthetic-contextual-anonymizer-dataset)

### Dataset Structure
- Training set: 3,456 examples
- Validation set: 432 examples
- Test set: 433 examples

Each example contains:
- `context`: Original text with sensitive information
- `anonymized_context`: Text with sensitive information replaced by tags
- `used_labels`: List of anonymization tag types used in the example

### Data Generation Process
The dataset was generated using:
1. OpenAI GPT models for diverse document generation
2. Custom anonymization rules
3. Consistent tag numbering system

## Supported Document Types

- Medical records
- Banking documents
- Business correspondence
- Recruitment documents
- Social media content
- Legal documents
- Educational records
- Insurance documents
- Chat conversations (personal, business, support)
- Email threads

## Anonymization Tags

The system supports various GDPR-compliant anonymization tags, including:
- [NAME] - Personal names
- [EMAIL] - Email addresses
- [PHONE] - Phone numbers
- [ADDRESS] - Physical addresses
- [PESEL] - Polish national ID numbers
- [NIP] - Polish tax identification numbers
- [DATE] - Dates
- [ACCOUNT] - Bank account numbers
- And many more domain-specific tags

## Getting Started

### Prerequisites
- Python 3.10+
- OpenAI API key
- Required packages from `requirements.txt`

### Installation
1. Clone the repository
```bash
git clone https://github.com/kurkowski93/contextual-anonymizer.git
cd contextual-anonymizer
```

2. Create and activate virtual environment
```bash
python -m venv venv
source venv/bin/activate
```

3. Install dependencies
```bash
pip install -r requirements.txt
```

4. Set up environment variables
```bash
cp .env.example .env
# Edit .env file with your OpenAI API key
```

## Usage Examples

### Loading the Dataset
```python
from datasets import load_dataset

dataset = load_dataset("kurkowski/synthetic-contextual-anonymizer-dataset")
```

### Example Data
```python
# Original text
print(dataset['train'][0]['context'])

# Anonymized version
print(dataset['train'][0]['anonymized_context'])
```

### Data Generation
1. Open `notebooks/synthetic_data.ipynb`
2. Configure document types and examples count in `doc_config`
3. Run all cells to generate synthetic training data
4. Generated data will be saved in `data/synthetic_data.json`

### Model Training and Evaluation
1. Open `notebooks/model_training_pipeline.ipynb`
2. Follow the complete pipeline from data loading to model evaluation
3. The notebook includes:
   - Data preprocessing with task-specific prompts
   - Training configuration options
   - Fine-tuning process
   - Comprehensive evaluation with multiple metrics
   - Visualization of results
   - Practical demo of the model in action

### Using the Model for Anonymization
```python
def generate_anonymization(text_to_anonymize, labels):
    prompt = create_anonymization_prompt(labels)
    inputs = tokenizer(
        prompt + text_to_anonymize, 
        return_tensors="pt",
        truncation=True
    )
    
    outputs = model.generate(
        input_ids=inputs["input_ids"],
        attention_mask=inputs["attention_mask"],
        max_length=512,
        temperature=0.1
    )
    return tokenizer.decode(outputs[0], skip_special_tokens=True)

# Example usage
sample_text = "On December 15, 2023, Jane Smith made a payment of $1,245.00 to ABC Corporation."
entity_types = ["NAME", "DATE", "MONEY_AMOUNT", "COMPANY"]
formatted_labels = [f"[{entity.upper()}]" for entity in entity_types]

anonymized = generate_anonymization(sample_text, formatted_labels)
print(anonymized)
# Output: "On [DATE_1], [NAME_1] made a payment of [MONEY_AMOUNT_1] to [COMPANY_1]."
```

## Model Evaluation Metrics

### Entity Recognition Metrics
- **Precision**: Measures the accuracy of anonymized entities in the output
- **Recall**: Measures how well the model identifies all sensitive entities
- **F1 Score**: Harmonic mean of precision and recall

### Text Similarity Metrics
- **BLEU Score**: Evaluates how well the model preserves n-gram sequences
- **ROUGE-L**: Measures the longest common subsequence to evaluate fluency

### Privacy Protection Metrics
- **Privacy breach detection**: Identifies if sensitive data appears in output
- **Global privacy protection rate**: Percentage of sensitive data properly anonymized
- **Per-entity leak analysis**: Detailed breakdown of which sensitive data types leak

## Development Roadmap

### Phase 1 (Completed)
- [x] Synthetic data generation pipeline
- [x] Dataset publication on Hugging Face Hub
- [x] Basic documentation

### Phase 2 (Completed)
- [x] Model training pipeline
- [x] Baseline model evaluation
- [x] Performance metrics implementation
- [x] Privacy-focused evaluation metrics

### Phase 3 (Planned)
- [ ] Inference API service
- [ ] Web-based demo interface
- [ ] Multi-language support
- [ ] Domain-specific model variants

## Troubleshooting

### Common Issues
1. **OpenAI API Rate Limits**
   - Solution: Implement appropriate delays between API calls
   - Use API key with sufficient quota

2. **Memory Issues During Data Generation**
   - Solution: Reduce batch size in synthetic data generation
   - Process data in smaller chunks

3. **Environment Setup**
   - Make sure to use Python 3.10+
   - Check if all dependencies are correctly installed


## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- OpenAI GPT for synthetic data generation
- Hugging Face Hub for dataset hosting
- Contributors and maintainers

## Environment Setup

1. Create a Python virtual environment:
   ```bash
   python -m venv venv
   ```

2. Activate the virtual environment:
   ```bash
   source venv/bin/activate
   ```

3. Install required packages:
   ```bash
   pip install -r requirements.txt
   ```