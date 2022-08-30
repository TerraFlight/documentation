# Fast API
FastAPI is a modern, fast (high-performance), web framework for building APIs with Python 3.6+ based on standard Python type hints.

### Possible Features
Whatever you can fit into a python package


## Simple [[Text Embeddings]] Snippet

```Python
import uvicorn
from fastapi import FastAPI
from pydantic import BaseModel
from starlette.responses import JSONResponse


class Data(BaseModel): # Define base model so Fast Api ain't crying
    text: str


app = FastAPI() # Define App Instance

from sentence_transformers import SentenceTransformer

model = SentenceTransformer('all-MiniLM-L6-v2') # Load pre-determined model


# Our endpoint for the encoding
@app.post("/embeds")
async def embed(input_data: Data):
    result = model.encode(input_data.text) # Encode 
    return JSONResponse(content=result.tolist()) # Use tolist here to make it serilizeable


if __name__ == '__main__':
    uvicorn.run('main:app', workers=1)
```
