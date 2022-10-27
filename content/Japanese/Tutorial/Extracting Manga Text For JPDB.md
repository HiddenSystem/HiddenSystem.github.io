# Extracting Manga Text For JPDB Using Mokuro

#### Step 1: Get raw images of Manga somehow
- If you have an Android Phone: see ![[Get Raw Manga Images From Tachiyomi]]
- If not, you're on your [own](../Resources/resources.md#random)

#### Step 2: Use Mokuro

Mokuro is a python OCR program for manga: [Mokuro](https://github.com/kha-white/mokuro)


1. (Optional but not really) Create a virtualenv for python 3.9, python 3.10 is not supported yet
    * `virtualenv -p python3 venv`
    * `source venv/bin/activate` or `source venv/Scripts/activate` if on Windows

2. (Optional) Install PyTorch with CUDA: [PyTorch](https://pytorch.org/get-started/locally/#start-locally)
    - Note: The command is wrong for pip at the moment, use this:
    - `pip3 install torch==1.12.1+cu116 torchvision==0.13.1+cu116 torchaudio==0.12.1+cu116 --extra-index-url https://download.pytorch.org/whl/cu116`
3. Install Mokuro `pip3 install mokuro`
4. Run Mokuro (Check Documentation for more info)
    - `mokuro --parent-dir "path/to/parent/dir"`
    - Note: OCR takes a while, the better your computer is, the faster it'll be

5. Congratulations, you now have a Yomichan-able html file
    - Note: For Yomichan, turn on the setting: Allow access to file URLs, and refresh the page

#### Step 3: Extract Text From JSON to use in JPDB

1. Use this dumb script, or something

```python
import glob
import json

output_filename = 'output.txt'
directory = r"path\to\directory\_ocr"

files = glob.glob(f"{directory}/**/*.json", recursive=False)
with open(output_filename,'w',encoding='utf-8') as out_file:
	for file in files:
		print(file)
		with open(file, 'r',encoding='utf-8') as f:
			input = json.load(f)
			for block in input["blocks"]:
				for line in block["lines"]:
					out_file.write(line + '\n')
```
   Paste that shit from `output.txt` in JPDB