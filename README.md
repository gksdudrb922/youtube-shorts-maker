# YouTube Shorts Maker

An AI-powered agent system for automatically creating vertical YouTube Shorts videos (9:16 portrait format) using Google ADK (Agent Development Kit).

## Overview

YouTube Shorts Maker is a multi-agent system that orchestrates the complete video creation workflow from concept to final MP4 output. It uses specialized AI agents working in sequence and parallel to generate content plans, create visual assets, produce audio narration, and assemble the final vertical video.

## Features

- **Automatic Content Planning**: AI-powered script generation with scene breakdowns
- **Parallel Asset Generation**: Simultaneously creates images and audio for efficiency
- **Vertical Video Optimization**: All assets are optimized for YouTube Shorts 9:16 format
- **Image Generation**: Uses OpenAI GPT-Image-1 API for vertical images with embedded text overlays
- **Text-to-Speech Narration**: Professional voice generation using OpenAI TTS API
- **Video Assembly**: Automated FFmpeg-based video stitching and encoding
- **Error Handling**: Robust error recovery and progress updates throughout the workflow

## Architecture

The system follows a hierarchical multi-agent architecture with the following components:

### Main Agent

**ShortsProducerAgent** (Root Agent)

- Orchestrates the entire video creation workflow
- Coordinates sub-agents in the correct sequence
- Provides user interaction and progress updates
- Handles error recovery

### Sub-Agents

#### 1. ContentPlannerAgent

- Creates structured content plans with scene breakdowns
- Generates narration text for each scene
- Designs visual descriptions optimized for image generation
- Plans embedded text overlays with positioning
- Ensures maximum 20-second duration constraint

#### 2. AssetGeneratorAgent (Parallel Agent)

Runs two specialized agents simultaneously:

- **ImageGeneratorAgent** (Sequential Agent)
  - **PromptBuilderAgent**: Transforms visual descriptions into optimized prompts with technical specs
  - **ImageBuilderAgent**: Generates vertical images using OpenAI GPT-Image-1 API

- **VoiceGeneratorAgent**
  - Selects appropriate voice based on content mood
  - Generates MP3 narration files using OpenAI TTS API

#### 3. VideoAssemblerAgent

- Assembles final video from generated assets
- Uses FFmpeg for video processing
- Handles timing, formatting, and encoding
- Outputs H.264/AAC MP4 format

## Requirements

- Python >= 3.13
- FFmpeg (for video assembly)
- OpenAI API key (for image generation and TTS)
- Google ADK dependencies

## Installation

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd youtube-shorts-maker
   ```

2. Install dependencies using uv:

   ```bash
   uv install
   ```

3. Set up your OpenAI API key:

   ```bash
   export OPENAI_API_KEY="your-api-key"
   ```

4. Ensure FFmpeg is installed:

   ```bash
   # macOS
   brew install ffmpeg

   # Ubuntu/Debian
   sudo apt-get install ffmpeg

   # Windows
   # Download from https://ffmpeg.org/download.html
   ```

## Usage

### Basic Usage

```python
from youtube_shorts_maker.agent import root_agent

# The agent will guide you through the video creation process
response = await root_agent.run(user_input="Create a YouTube Short about making perfect scrambled eggs")
```

### Workflow

1. **User Input**: Provide topic, style, and requirements
2. **Content Planning**: Agent creates structured script with scenes
3. **Asset Generation**: Images and audio generated in parallel
4. **Video Assembly**: All assets combined into final MP4
5. **Delivery**: Final video artifact available for download

## Technical Specifications

### Video Format

- Resolution: 1080x1920 (9:16 portrait)
- Frame Rate: 30fps
- Codec: H.264 (video), AAC (audio)
- Maximum Duration: 20 seconds
- Format: MP4

### Image Specifications

- Resolution: 1024x1536 (9:16 portrait)
- Format: JPEG
- Embedded Text: Positioned overlays with generous padding
- Quality: Professional, photorealistic

### Audio Specifications

- Format: MP3
- Voices: alloy, echo, fable, onyx, nova, shimmer
- Model: gpt-4o-mini-tts

## Project Structure

```text
youtube_shorts_maker/
├── agent.py                 # Main root agent
├── prompt.py                # Main agent prompts
├── sub_agents/
│   ├── content_planner/
│   │   ├── agent.py        # Content planning agent
│   │   └── prompt.py       # Content planning prompts
│   ├── asset_generator/
│   │   ├── agent.py        # Parallel asset generator
│   │   ├── prompt.py       # Asset generator prompts
│   │   ├── image_generator/
│   │   │   ├── image_builder/
│   │   │   │   ├── agent.py
│   │   │   │   ├── prompt.py
│   │   │   │   └── tools.py # Image generation tools
│   │   │   └── prompt_builder/
│   │   │       ├── agent.py
│   │   │       └── prompt.py
│   │   └── voice_generator/
│   │       ├── agent.py
│   │       ├── prompt.py
│   │       └── tools.py    # Voice generation tools
│   └── video_assembler/
│       ├── agent.py        # Video assembly agent
│       ├── prompt.py       # Assembly prompts
│       └── tools.py        # FFmpeg video tools
```

## Dependencies

- `google-adk` >= 1.12.0 - Agent Development Kit
- `google-genai` >= 1.31.0 - Google Generative AI
- `litellm` >= 1.76.0 - LLM abstraction layer
- `openai` >= 1.101.0 - OpenAI API client

## License

License information not specified. Please check with the project maintainers for licensing details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

Built with Google ADK (Agent Development Kit) and powered by OpenAI's GPT-4 and GPT-Image-1 models.
