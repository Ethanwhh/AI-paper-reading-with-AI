# GUI Agents: A Survey


## Mind map

! [Mind map](... /imgs/GUI-Agents-A-Survey.png)


## Main content

### 1. Author and team information

** Author ** : Dang Nguyen (University of Maryland), Jian Chen (State University of New York at Buffalo), Yu Wang (University of Oregon), Gang Wu (Adobe Research) and 33 other authors from 11 institutions, Including universities (such as the University of California San Diego, Carnegie Mellon University), enterprise laboratories (such as Adobe Research, Meta AI, Intel AI Research).

** Team Profile ** : Lead authors Dang Nguyen (University of Maryland) and Gang Wu (Adobe Research) have long worked on intelligent agent and GUI interactions, and the team integrates experts in computer vision, natural language processing, and human-computer interaction to advance the systematic study of GUI agents.

### 2. Background and motivation

** Publication Date ** : December 2024 (arXiv preprint)

** Research Question ** : How efficiently and robustly can GUI agents based on Large Base Models (LFMs) automate human-computer interaction through Graphical user interfaces (GUIs)?

** Background and Opportunity ** :

- LFMs are shifting from conversational chatbots to task execution agents, with GUIs as the core interface for human-computer interaction, and the need for automation is growing.

- There are challenges in GUI environments such as dynamic layout, cross-platform diversity, and fine-grained element positioning, and existing research is fragmented and lacks a unified framework.

- Industry (such as Anthropic, OpenAI) is interested in GUI agents, but the academic community has not yet formed a systematic summary.

### 3. Relevant research

** Previous methods ** :

- ** Benchmark construction ** : Static datasets (e.g. RUSS, Mind2Web) and interactive environments (e.g. MiniWoB, WebShop) are used to evaluate agent performance, but closed world assumptions limit generalization and open world environments are difficult to reproduce.

- ** Architecture Design ** : Perception module relies on accessibility API, HTML/DOM parsing or screen vision; Planning module combined with LLM internal knowledge or external tools (such as A * search); Action modules perform actions via text or visual grounding.

- ** Training Method ** : Prompt engineering (dynamic action generation, self-reflection) and parameter optimization (pre-training, fine-tuning, reinforcement learning) to improve agent capability.

** Lack of **:

- Lack of a unified framework to integrate perception, reasoning, planning, and action.

- Problems such as user intent understanding, security and privacy, and inference delay in open world scenarios are not fully solved.

- Existing evaluation indicators focus on task completion and lack fine-grained analysis of intermediate steps and robustness.

### 4. Core ideas

** Core idea ** : Proposes a unified framework for GUI agents, divides their capabilities into four modules: ** perception **, ** reasoning **, ** planning **, ** action **, systematically classifies existing benchmarks, architectures and training methods, and identifies key challenges.

** Idea Source ** :

- Observed that GUI agents need to imitate human visual and interactive operations to complete tasks, and need to integrate multimodal perception (visual, text) and decision reasoning.

- Draw on reinforcement learning (POMDP modeling) and LLM-driven agent architecture, combined with the unique requirements of GUI interaction (such as element localization, cross-platform adaptation).

### 5. Programme and technology

** Base classification **

- ** Static Data set ** :

  - Closed world (e.g. TURKINGBENCH) : fine-grained assessment, reproducible, but not dynamic.

  - Open world (e.g. GAIA) : Real website interaction, assessment of adaptability, difficult to reproduce.

- ** Interactive Environment ** :

  - Closed world (e.g. WebArena) : controlled simulation with support for multi-step workflows.

  - Open world (e.g. WebVoyager) : Dynamic real-world environments that test robustness.

- ** Evaluation indicators ** : Task completion rate, intermediate step accuracy (URL/element matching), efficiency, safety.

** Architecture Design **

1. ** Sensing module ** :

  - Accessibility apis (system-level semantic parsing, such as the Android Accessibility API).

  - HTML/DOM parsing (page structure analysis, such as DOM ranking of Mind2Web).

  - Screen vision (screenshot recognition, e.g. GPT-4V parsing UI elements).

  - Hybrid interface (multi-modal fusion, such as OS-Atlas combining vision and text).

2. ** Reasoning and Planning ** :

  - Inside knowledge: LLM simulated action results (WebDreamer), hierarchy planning (MobA).

  - External knowledge: A combination of search algorithms (A*, MCTS) or Toolchain*.

3. ** Action Module ** :

  - Textual grounding (DOM/API based element positioning) or visual grounding (pixel level coordinate positioning).

** Training method **

- ** Tips - based** : Dynamic generation of Python code (DynaSaur), self-reflective optimization (Agent Q).

- ** Training - based** :

  - Pre-training: multi-modal model (such as PIX2STRUCT analysis screenshot).

  - Fine tuning: Reduce illusion (Falcon-UI), cross-platform grounding (UGround).

  - Reinforcement learning: dealing with sparse rewards (WebRL), online course learning (AutoGLM).

### 6. Experiment and summary

** Experimental Design ** :

- A review paper, no specific experiments, but a collation of evaluation results from existing benchmarks (e.g., WebVoyager task completion rate of 85.3%, consistent with human judgment), architectural comparison (hybrid interface is better than single mode), and training method effectiveness (reinforcement learning improves long-term task performance).

** Conclusion ** :

- GUI agents perform well in closed world tasks, but open world generalization, security, and efficiency still need to be improved.

- The unified framework provides systematic guidance for subsequent research, with multi-modal fusion and lightweight models as key directions.

### 7. Major contribution

1. ** Unified framework ** : For the first time, the GUI agent is divided into four modules: perception, reasoning, planning, and action, and the technical path of each module is clear.

2. ** Benchmark classification ** : Systematically collates 30 + data sets and environments, differentiates closed/open world scenarios, and provides evaluation index systems.

3. **Challenge identification ** : Points out key issues such as user intent understanding, security and privacy, and inference delay, and points out the direction for future research.

### 8. Deficiencies and future directions

** Lack of **:

- Not covering command line interface (CLI) and API-driven agents, focusing on GUI scenarios.

- Limited discussion on the frontiers of long-term memory and multi-agent collaboration.

** Future Direction ** :

- Improve open world generalization, study small sample adaptation and dynamic environment robustness.

- Develop privacy protection technologies (e.g., federated learning, local computing) to reduce the risk of data transmission.

- Optimize model efficiency with hardware acceleration for real-time interaction.


## Code implementation

The following is the Python pseudo-code based on the paper framework, simulating the core flow of the GUI agent:

```python
from langchain.llms import OpenAI
from PIL import Image
import cv2
import numpy as np

class GUIAgent:
def __init__(self):
self.llm = OpenAI(temperature=0.7) # Assume inference planning using LLM
self.perception_modules = {
accessibility: AccessibilityAPI(), # accessibility API
"dom": DOMParser(), # DOM parser
"visual": VisualParser() # Visual parser (e.g. OCR, object detection)
}

def perceive(self, env_type, screenshot=None, dom=None):
"" Multimodal perception ""
if env_type == "web":
dom_info = self.perception_modules["dom"].parse(dom)
visual_info = self.perception_modules["visual"].analyze(screenshot)
return {**dom_info, **visual_info}
elif env_type == "mobile":
return self.perception_modules["accessibility"].get_elements()
return {}

def plan(self, task, current_state):
"" LLM-Driven Mission Planning """
prompt = f" task: {task}, current interface element: {current_state}, generate next action sequence"
action_plan = self.llm(prompt)
return action_plan.split("\n") # Split into subtasks

def act(self, action, element):
""" Perform action (simulate click/input) """
if action == "click":
print(f" Click on element: {element['label']} (coordinate: {element['coords']}) ")
elif action == "type":
Print (f "input text: {element [' text ']} to {element [' label ']}")

def run(self, task, env_type, screenshot=None, dom=None):
""" Complete process: Perception → Planning → Action ""
state = self.perceive(env_type, screenshot, dom)
plan = self.plan(task, state)
for action in plan:
element = self._select_element(action, state) # Simplified element selection logic
self.act(action, element)

def _select_element(self, action_desc, state):
""" Select UI elements based on action description (simplify logic) """
for elem in state["elements"]:
if action_desc in elem["label"].lower():
return elem
return state["elements"][0] # The first element is selected by default

# Example: Simulated web task (Search for products)
agent = GUIAgent()
screenshot = Image.open("screenshot.png") # Assume a screenshot
Dom = "< HTML > < body > < button > search < / button > < input id = 'search - box' / > < / body > < / HTML >"
agent.run(" Search Laptop ", "web", screenshot, dom)
` ` `

** Code Description ** :

- Perception module: Supports web (DOM + vision) and mobile (accessibility API) environments, integrating multi-modal input.

- Planning module: Use LLM to generate action sequences, depending on task description and current interface state.

- Action module: Simulates click/enter actions to locate UI elements by element tags or coordinates.

- Process integration: Use the run method to connect perception, planning, and action to achieve end-to-end task execution.

The code simplifies the core logic in the paper, and practical application requires a combination of specific data sets (such as WebArena) and training methods (such as reinforcement learning to optimize action strategies).
