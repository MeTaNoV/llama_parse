# LlamaParse

LlamaParse is an API created by LlamaIndex to efficiently parse and represent files for efficient retrieval and context augmentation using LlamaIndex frameworks.

LlamaParse directly integrates with [LlamaIndex](https://github.com/run-llama/llama_index).

Currently available in preview mode for **free**. Try it out today!

**NOTE:** Currently, only PDF files are supported.

## Getting Started

First, login and get an api-key from `https://cloud.llamaindex.ai`.

Then, make sure you have the latest LlamaIndex version installed.

**NOTE:** If you are upgrading from v0.9.X, we recommend following our [migration guide](https://pretty-sodium-5e0.notion.site/v0-10-0-Migration-Guide-6ede431dcb8841b09ea171e7f133bd77), as well as uninstalling your previous version first.

```
pip uninstall llama-index  # run this if upgrading from v0.9.x or older
pip install -U llama-index --upgrade --no-cache-dir --force-reinstall
```

Lastly, install the package:

`pip install llama-parse`

Now you can run the following to parse your first PDF file:

```python
import nest_asyncio
nest_asyncio.apply()

from llama_parse import LlamaParse

parser = LlamaParse(
    api_key="llx-...",  # can also be set in your env as LLAMA_CLOUD_API_KEY
    result_type="markdown",  # "markdown" and "text" are available
    num_workers=4, # if multiple files passed, split in `num_workers` API calls
    verbose=True
)

# sync
documents = parser.load_data("./my_file.pdf")

# sync batch
documents = parser.load_data(["./my_file1.pdf", "./my_file2.pdf"])

# async
documents = await parser.aload_data("./my_file.pdf")

# async batch
documents = await parser.aload_data(["./my_file1.pdf", "./my_file2.pdf"])
```

## Using with `SimpleDirectoryReader`

You can also integrate the parser as the default PDF loader in `SimpleDirectoryReader`:

```python
import nest_asyncio
nest_asyncio.apply()

from llama_parse import LlamaParse
from llama_index.core import SimpleDirectoryReader

parser = LlamaParse(
    api_key="llx-...",  # can also be set in your env as LLAMA_CLOUD_API_KEY
    result_type="markdown",  # "markdown" and "text" are available
    verbose=True
)

file_extractor = {".pdf": parser}
documents = SimpleDirectoryReader("./data", file_extractor=file_extractor).load_data()
```

Full documentation for `SimpleDirectoryReader` can be found on the [LlamaIndex Documentation](https://docs.llamaindex.ai/en/stable/module_guides/loading/simpledirectoryreader.html).

## Examples

Several end-to-end indexing examples can be found in the examples folder

- [Getting Started](examples/demo_basic.ipynb)
- [Advanced RAG Example](examples/demo_advanced.ipynb)
- [Raw API Usage](examples/demo_api.ipynb)

## Terms of Service

See the [Terms of Service Here](./TOS.pdf).
