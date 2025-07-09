# Understanding LLM Decision Making: Token Probabilities and Perplexity

> **Interactive notebooks exploring how Large Language Models make probabilistic decisions and why prompt design matters**

This repository contains practical, hands-on explorations of how Large Language Models (LLMs) generate text through token-by-token probability decisions. Using OpenAI's API with logprobs, we visualize model confidence, temperature effects, and demonstrate how subtle prompt changes can dramatically affect model behavior.

## 🎯 What You'll Learn

- **How LLMs think**: See token-by-token probability decisions in real-time
- **Temperature effects**: Understand why the same prompt gives different answers
- **Prompt sensitivity**: Discover how tiny wording changes affect model confidence
- **Perplexity as insight**: Use perplexity scores to understand model uncertainty
- **Structural failures**: Watch models break under conflicting instructions

## 📊 Key Insights

Based on recent research (["Demystifying Prompts in Language Models via Perplexity Estimation"](https://arxiv.org/abs/2212.04037)), this work demonstrates:

- **Lower perplexity prompts perform better** - Models are more confident with familiar language patterns
- **Temperature doesn't just add randomness** - It reveals underlying uncertainty in model decisions  
- **Prompt engineering is probabilistic** - Small changes can cause dramatic confidence shifts
- **Structural breakdowns are predictable** - High perplexity signals when models will fail

## 🚀 Quick Start

### Prerequisites

```bash
# Python 3.8+
pip install openai matplotlib seaborn numpy pandas ipywidgets
```

### API Setup

1. Get an OpenAI API key from [OpenAI Platform](https://platform.openai.com/api-keys)
2. Create a `config.json` file in the repository root:

```json
{
  "openai_api_key": "your-api-key-here"
}
```

### Running the Notebooks

#### Option 1: Local Jupyter
```bash
git clone https://github.com/yourusername/perplexityViews
cd perplexityViews
jupyter lab
```

#### Option 2: Google Colab
1. Upload the `.ipynb` files to Google Drive
2. Open with Google Colab
3. Install dependencies: `!pip install openai matplotlib seaborn ipywidgets`
4. Modify the config loading to use Colab secrets or direct input

#### Option 3: JupyterLab
```bash
pip install jupyterlab
jupyter lab
```

## 📚 Notebooks Overview

### 1. `token_probability_viz.ipynb` - Complete Exploration
**The full research notebook** - Comprehensive analysis with:
- Token probability extraction and visualization
- Temperature effects across different prompt types
- Structured JSON output analysis  
- Conflicting instructions that break model behavior
- Advanced visualizations and pattern analysis

**Best for**: Understanding the complete research process and methodology

### 2. `simple_perplexity.ipynb` - Interactive Comparison Tool
**The practical tool** - Clean, focused interface with:
- Interactive widgets for easy experimentation
- Simple perplexity calculation and comparison
- Clean tabular output for prompt analysis
- Temperature and prompt comparison functions

**Best for**: Quick experiments and demonstrating concepts to others

## 🎮 Interactive Features

Both notebooks include interactive widgets that let you:

- **Compare temperatures**: See how the same prompt behaves at different temperature settings
- **Test prompt variations**: Experiment with subtle wording changes  
- **Real-time perplexity**: Calculate confidence scores instantly
- **Conflict scenarios**: Create impossible prompts that force model failures

### Example Interactive Usage

```python
# Temperature comparison
@interact(
    prompt=Text("The capital of France is"),
    temp1=FloatSlider(0.1, min=0.0, max=2.0),
    temp2=FloatSlider(0.7, min=0.0, max=2.0),
    temp3=FloatSlider(1.5, min=0.0, max=2.0)
)
def compare_temperatures(prompt, temp1, temp2, temp3):
    # Interactive comparison with real-time results
```

## 🧪 Key Experiments

### Temperature Effects
Demonstrates how temperature affects model confidence across different prompt types:
- **Factual prompts** (e.g., "The capital of France is") remain stable
- **Creative prompts** (e.g., "The best programming language is") show more variation
- **Ambiguous prompts** (e.g., "Today is") reveal interesting patterns

### Conflicting Instructions
Shows what happens when prompts contain impossible requirements:
```
"Use this exact JSON format with no deviation:
{task: string, priority: string, deadline: string}

Create a task with attendee list and agenda items."
```
Result: Model breaks at high temperatures, producing invalid JSON

### Prompt Sensitivity
Reveals how tiny changes affect model behavior:
- "The best programming language is" vs "The most popular programming language is"
- "Today is" vs "The current date is"
- Punctuation effects: "The answer is" vs "The answer is:"

## 📈 Understanding the Output

### Perplexity Interpretation
- **1-2**: Very predictable (factual completions)
- **2-10**: Somewhat predictable  
- **10-100**: Moderately uncertain
- **100+**: High uncertainty/ambiguity
- **1000+**: Very confused/ambiguous prompt

### Confidence Colors
- 🟢 **Dark Green**: Very high confidence (>0.95)
- 🟢 **Light Green**: High confidence (0.8-0.95)
- 🟡 **Yellow**: Medium confidence (0.6-0.8)
- 🟠 **Orange**: Low confidence (0.4-0.6)
- 🔴 **Red**: Very low confidence (<0.4)

## 🔬 Research Applications

This work supports research in:
- **Prompt engineering**: Understanding why certain prompts work better
- **Model reliability**: Predicting when models will fail
- **Agentic systems**: Building robust AI agents that handle uncertainty
- **Human-AI interaction**: Designing better interfaces that show model confidence

## 🛠️ Technical Details

### Dependencies
- `openai>=1.0.0` - API access and logprobs
- `matplotlib>=3.5.0` - Visualizations
- `seaborn>=0.11.0` - Statistical plotting
- `numpy>=1.21.0` - Numerical operations
- `pandas>=1.3.0` - Data manipulation
- `ipywidgets>=7.6.0` - Interactive controls

### API Usage
The notebooks use OpenAI's Chat Completions API with:
- `logprobs=True` - Token probability access
- `top_logprobs=5` - Alternative token probabilities
- `temperature` variations - Controlling randomness
- `max_tokens` - Response length limits

### Performance Notes
- Each API call costs according to OpenAI pricing
- Perplexity calculations require token-level probability data
- Interactive widgets make multiple API calls - monitor usage
- Consider rate limits for extensive experimentation

## 📖 Background Reading

### Core Research
- [Demystifying Prompts in Language Models via Perplexity Estimation](https://arxiv.org/abs/2212.04037) - The foundational paper showing perplexity predicts prompt performance
- [Language Model Evaluation Beyond Perplexity](https://arxiv.org/abs/2106.00085) - Limitations of perplexity as a metric

### Related Work
- [What is Wrong with Perplexity for Long-context Language Modeling?](https://arxiv.org/abs/2410.23771) - Recent findings on perplexity limitations
- [Can Perplexity Reflect Large Language Model's Ability in Long Text Understanding?](https://arxiv.org/abs/2405.06105) - Perplexity vs. understanding

## 🤝 Contributing

Contributions welcome! Areas of interest:
- Additional prompt types and experiments
- New visualization techniques
- Alternative perplexity calculations
- Integration with other LLM APIs
- Educational improvements

### Getting Started
1. Fork the repository
2. Create a feature branch
3. Add your experiments or improvements
4. Submit a pull request with clear documentation

## ⚠️ Important Notes

### API Costs
- Each prompt generates API costs
- Monitor your OpenAI usage dashboard
- Start with small experiments before scaling
- Consider using smaller models (gpt-3.5-turbo) for initial exploration

### Educational Use
- These notebooks are designed for learning and research
- Results may vary with different models and API versions
- Always verify findings with multiple experiments
- Be mindful of API rate limits during classroom use

## 📜 License

MIT License - Feel free to use for research, education, and commercial applications.

## 🙏 Acknowledgments

- **OpenAI** for API access and logprobs functionality
- **Hila Gonen et al.** for the foundational perplexity research
- **Jupyter** ecosystem for interactive development
- **Community** feedback and contributions

## 📬 Contact

Questions? Ideas? Found a bug?
- Create an issue in this repository
- Connect on LinkedIn: [Your LinkedIn Profile]
- Follow the research: [Your preferred contact method]

---

*Built with curiosity about how LLMs really think. Dive in and discover the probabilistic nature of AI decision-making!*
