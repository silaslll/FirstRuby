"""
Test script to generate a specific 8x8 slide with a text box.
Reference: src/agents/renderer.py and src/layout/text_height_measurement.py

"""

import sys
from pathlib import Path
from pptx import Presentation
from pptx.util import Inches, Pt
from pptx.enum.text import MSO_AUTO_SIZE, PP_ALIGN
from pptx.dml.color import RGBColor

# Add project root to sys.path to allow imports from src
project_root = Path(__file__).parent.parent.parent
if str(project_root) not in sys.path:
    sys.path.append(str(project_root))

from src.config.poster_config import load_config

def main():
    # Load config to follow conventions if needed, though specific requirements are hardcoded
    config = load_config()

    # Create presentation
    prs = Presentation()
    
    boxheight = 2

    #修改宽度来测试
    boxwidth = 33.99

    prs.slide_width = Inches(boxwidth+ 1)
    prs.slide_height = Inches(boxheight+1)

    # Add a blank slide
    # layout 6 is usually blank
    slide = prs.slides.add_slide(prs.slide_layouts[6])

    tx_box = slide.shapes.add_textbox(
        Inches(0), Inches(0), Inches(boxwidth), Inches(boxheight)
    )

    # Configure text frame
    tf = tx_box.text_frame
    tf.word_wrap = True
    tf.auto_size = MSO_AUTO_SIZE.NONE
    
    tf.margin_left = 0
    tf.margin_right = 0
    tf.margin_top = 0
    tf.margin_bottom = 0

    p = tf.paragraphs[0]
    p.font.size = Pt(26)
    p.font.name = "Arial" # Standard default
    p.font.bold = False

    # ==========================================
    # 测试每种character 的宽度， 每次测试一种character
    # ==========================================

    # --- Lowercase Letters ---
    p.text = "a" * 100
    # p.text = "b" * 100
    # p.text = "c" * 100
    # p.text = "d" * 100
    # p.text = "e" * 100
    # p.text = "f" * 100
    # p.text = "g" * 100
    # p.text = "h" * 100
    # p.text = "i" * 100
    # p.text = "j" * 100
    # p.text = "k" * 100
    # p.text = "l" * 100
    # p.text = "m" * 100
    # p.text = "n" * 100
    # p.text = "o" * 100
    # p.text = "p" * 100
    # p.text = "q" * 100
    # p.text = "r" * 100
    # p.text = "s" * 100
    # p.text = "t" * 100
    # p.text = "u" * 100
    # p.text = "v" * 100
    # p.text = "w" * 100
    # p.text = "x" * 100
    # p.text = "y" * 100
    # p.text = "z" * 100

    # --- Numbers ---
    # p.text = "0" * 100
    # p.text = "1" * 100
    # p.text = "2" * 100
    # p.text = "3" * 100
    # p.text = "4" * 100
    # p.text = "5" * 100
    # p.text = "6" * 100
    # p.text = "7" * 100
    # p.text = "8" * 100
    # p.text = "9" * 100

    # --- Special Characters ---
    # p.text = "!" * 100
    # p.text = "@" * 100
    # p.text = "#" * 100
    # p.text = "$" * 100
    # p.text = "%" * 100
    # p.text = "^" * 100
    # p.text = "&" * 100
    # p.text = "*" * 100
    # p.text = "(" * 100
    # p.text = ")" * 100
    # p.text = "_" * 100
    # p.text = "+" * 100
    # p.text = "-" * 100
    # p.text = "=" * 100
    # p.text = "[" * 100
    # p.text = "]" * 100
    # p.text = "{" * 100
    # p.text = "}" * 100
    # p.text = "\\" * 100
    # p.text = "|" * 100
    # p.text = "/" * 100
    # p.text = "?" * 100
    # p.text = "’" * 100
    # p.text = "”" * 100
    # p.text = ":" * 100
    # p.text = ";" * 100
    # p.text = "," * 100
    # p.text = "." * 100
    # p.text = "`" * 100
    # p.text = "~" * 100

    # --- Bold Lowercase Letters ---
    # p.text = "a" * 100; p.font.bold = True
    # p.text = "b" * 100; p.font.bold = True
    # p.text = "c" * 100; p.font.bold = True
    # p.text = "d" * 100; p.font.bold = True
    # p.text = "e" * 100; p.font.bold = True
    # p.text = "f" * 100; p.font.bold = True
    # p.text = "g" * 100; p.font.bold = True
    # p.text = "h" * 100; p.font.bold = True
    # p.text = "i" * 100; p.font.bold = True
    # p.text = "j" * 100; p.font.bold = True
    # p.text = "k" * 100; p.font.bold = True
    # p.text = "l" * 100; p.font.bold = True
    # p.text = "m" * 100; p.font.bold = True
    # p.text = "n" * 100; p.font.bold = True
    # p.text = "o" * 100; p.font.bold = True
    # p.text = "p" * 100; p.font.bold = True
    # p.text = "q" * 100; p.font.bold = True
    # p.text = "r" * 100; p.font.bold = True
    # p.text = "s" * 100; p.font.bold = True
    # p.text = "t" * 100; p.font.bold = True
    # p.text = "u" * 100; p.font.bold = True
    # p.text = "v" * 100; p.font.bold = True
    # p.text = "w" * 100; p.font.bold = True
    # p.text = "x" * 100; p.font.bold = True
    # p.text = "y" * 100; p.font.bold = True
    # p.text = "z" * 100; p.font.bold = True

    # Output path
    output_dir = project_root / "output" / "font_metrics"
    output_dir.mkdir(parents=True, exist_ok=True)
    output_path = output_dir / "test_render_box.pptx"

    prs.save(output_path)
    print(f"Saved test presentation to: {output_path}")





langgraph>=0.2.45
langchain>=0.3.0
langchain-openai>=0.2.0
langchain-anthropic>=0.2.0
langchain-google-genai>=2.0.0
langchain-community>=0.3.0
docling>=2.7.1
docling-core>=2.3.0
python-pptx>=1.0.2
Pillow>=10.0.0
opencv-python>=4.8.0
PyMuPDF>=1.24.0
pypdf>=5.0.0
pdfminer.six==20231228
pymupdf4llm>=0.0.17
requests>=2.32.0
beautifulsoup4>=4.12.0
urllib3>=2.0.0
torch==2.7.1
torchvision==0.22.1
transformers==4.52.4
diffusers>=0.25.0
accelerate>=0.30.0
easyocr>=1.7.0
numpy>=1.24.0
pandas>=2.0.0
datasets>=3.0.0
scikit-learn>=1.3.0
python-dotenv>=1.0.0
Jinja2>=3.1.0
pydantic>=2.0.0
tenacity>=8.0.0
typing-extensions>=4.8.0
tqdm>=4.66.0
imageio>=2.34.0
ffmpeg-python>=0.2.0
jupyter>=1.1.0
matplotlib>=3.7.0
seaborn>=0.12.0
aiohttp>=3.9.0
aiofiles>=24.0.0
pytest>=8.0.0
pytest-asyncio>=0.24.0
jsonschema>=4.20.0
pyyaml>=6.0.0
markdown>=3.5.0
json_repair==0.35.0
git+https://github.com/Hadlay-Zhang/marker.git
pypandoc
qrcode[pil]
fastapi>=0.104.0
uvicorn>=0.24.0
python-multipart>=0.0.6

https://www.rapidtables.com/web/tools/pixel-ruler.html

### Initial Setup

```bash
# 1. Install Python 3.11
brew install python@3.11

# 2. Navigate to project directory
cd /path/to/your/project

# 3. Create virtual environment with Python 3.11
python3.11 -m venv .venv

# 4. Activate virtual environment
source .venv/bin/activate

# 5. Install dependencies
pip install -e .

```

### Daily Usage






if __name__ == "__main__":
    main()
