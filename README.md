# Contextual Text Anonymizer

A comprehensive pipeline for training and deploying text anonymization models with contextual understanding. This project aims to create a robust system for identifying and anonymizing sensitive information in various types of documents while preserving the context and readability of the text.

## Project Structure

1. **Data Generation** (`notebooks/synthetic_data.ipynb`)
   - Generates synthetic training data using GPT models
   - Creates pairs of original and anonymized text
   - Supports multiple document types (medical, banking, business, etc.)
   - Maintains consistent anonymization tags with numerical suffixes

2. **Training Pipeline** (coming soon)
   - Model training scripts and configurations
   - Fine-tuning procedures
   - Evaluation metrics

3. **Inference Service** (coming soon)
   - API for text anonymization
   - Batch processing capabilities
   - Performance optimization

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
source venv/bin/activate  # On Windows: venv\Scripts\activate
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

## Development Roadmap

### Phase 1 (Completed)
- [x] Synthetic data generation pipeline
- [x] Dataset publication on Hugging Face Hub
- [x] Basic documentation

### Phase 2 (In Progress)
- [ ] Model training pipeline
- [ ] Baseline model evaluation
- [ ] Performance metrics implementation

### Phase 3 (Planned)
- [ ] ?

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
   