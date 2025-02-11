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

### Data Generation
1. Open `notebooks/synthetic_data.ipynb`
2. Configure document types and examples count in `doc_config`
3. Run all cells to generate synthetic training data
4. Generated data will be saved in `data/synthetic_data.json`

## Project Status

- [x] Synthetic data generation pipeline
- [ ] Model training pipeline
- [ ] Inference service
- [ ] API documentation
- [ ] Performance optimization
- [ ] Production deployment guide

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- OpenAI GPT for synthetic data generation
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
   