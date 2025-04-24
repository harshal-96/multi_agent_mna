# MNA Multi-Agent Analysis System

A sophisticated multi-agent framework for comprehensive Mergers & Acquisitions analysis using LlamaIndex and OpenAI. This system orchestrates specialized AI agents to analyze acquisition targets across multiple dimensions, producing structured reports and decision matrices to support M&A decisions.

## Overview

This framework implements a workflow of specialized AI agents, each focusing on a specific aspect of M&A analysis:

- **Target Identification**: Evaluates potential acquisition targets based on specified criteria
- **Financial Analysis**: Assesses financial compatibility, health, and risks
- **Strategic Fit**: Evaluates alignment, product portfolio fit, and market synergies
- **Legal Risk Assessment**: Identifies antitrust concerns, regulatory requirements, and compliance issues
- **Market Sentiment Analysis**: Analyzes media coverage, analyst opinions, and stakeholder sentiments
- **Synergy Estimation**: Estimates revenue, cost, financial, and strategic synergies
- **Deal Structuring**: Recommends optimal transaction type and terms
- **Valuation**: Performs multiple valuation methods and recommends price ranges
- **Report Generation**: Compiles analyses into a comprehensive report
- **Report Review**: Creates a weighted decision matrix for final recommendation

## Requirements

- Python 3.8+
- OpenAI API key
- Tavily API key (for web search capabilities)

## Installation

```bash
pip install llama-index
pip install tavily-python
pip install llama-index-utils-workflow
pip install yfinance
```

## Configuration

Set up your API keys:

```python
# Using Google Colab
from google.colab import userdata
api_key = userdata.get('OPEN_AI_API_KEY')
tavily_api_key = userdata.get('TAVILY_API_KEY')

# Alternatively, for local development
import os
api_key = os.environ.get('OPENAI_API_KEY')
tavily_api_key = os.environ.get('TAVILY_API_KEY')
```

## Usage

### Basic Usage

```python
# Initialize the workflow
mna_workflow = MnAAnalysisWorkflow(timeout=300, verbose=True)

# Run the workflow
handler = mna_workflow.run(
    criteria="Luxury fashion brand with strong global recognition, annual revenue > $500M, profitable, positioned in the high-end/luxury market segment, and with complementary product lines or geographic market reach",
    industry="Fashion",
    acquirer_company="Prada",
    target_company="Versace",
    target_id_agent=target_identification_agent,
    financial_agent=financial_analysis_agent,
    strategic_agent=strategic_fit_agent,
    legal_agent=legal_risk_agent,
    sentiment_agent=sentiment_agent,
    synergy_agent=synergy_agent,
    deal_agent=deal_structure_agent,
    valuation_agent=valuation_agent,
    report_agent=report_agent,
    review_agent=review_agent
)

# Get final result
final_result = await handler
print("\n==== COMPLETE M&A ANALYSIS REPORT ====")
print(final_result)
```

### Monitoring Progress

```python
# Stream and display events
async for ev in handler.stream_events():
    if isinstance(ev, TargetIdentificationEvent):
        print(f"🔍 Identifying target: {ev.target_company} based on criteria: {ev.criteria} in {ev.industry}")
    elif isinstance(ev, FinancialAnalysisEvent):
        print(f"💰 Analyzing financials for {ev.target_company} and {ev.acquirer_company}")
    # More event handlers...
```

### Workflow Visualization

```python
from llama_index.utils.workflow import draw_all_possible_flows
draw_all_possible_flows(mna_workflow, filename="workflow.html")
```

## System Architecture

The system is built on a workflow orchestration pattern:

1. **Tools**: Web search functionality via Tavily API
2. **Specialized Agents**: Function-calling agents with specific system prompts
3. **Events**: Structured data objects for passing information between workflow steps
4. **Workflow**: Sequential execution of analysis steps with data aggregation

## Example Output

The system produces a comprehensive M&A analysis report with sections including:

- Target company profile
- Financial analysis
- Strategic fit evaluation
- Legal and regulatory risks
- Market sentiment analysis
- Synergy estimation
- Deal structure recommendation
- Valuation analysis
- Executive summary
- Decision matrix with final recommendation

## Customization

This framework is designed to be flexible and adaptable:

- Modify system prompts to adjust agent behavior
- Add new specialized agents for additional analysis dimensions
- Adapt to different industries by changing search queries
- Adjust the weighting factors in the decision matrix
- Integrate additional data sources beyond web search

## Limitations

- Quality of analysis depends on available web information
- Search results may not include the most recent data
- Analysis depth is constrained by the LLM's capabilities
- Web search may sometimes return irrelevant information

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
