# tool-transformer-split-rows

Splits a delimited row value into two output fields using a configurable separator.

## Behavior

The transformer reads the string under `value` in each mapped row and returns
fields `a` and `b`. The `delimiter` hyperparameter defaults to `|`.

- `hello|world` becomes `{"a": "hello", "b": "world"}`.
- A value without the separator produces an empty `b`.
- If there are more than two parts, only the first two are returned.
- The number of input rows stays the same.

Configure row mappings with `input_mapping={"value": "source_column"}` and
`return_mapping={"a": "first_column", "b": "second_column"}`. Leave `column`
unset to use row transformation mode.

## Development

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements-dev.txt
cp .env.example .env
# Set APP_ID and platform URLs in .env before connecting.
python main.py
```

The Docker base image provides the FL-Net API. `requirements.txt` contains only
additional runtime dependencies; `requirements-dev.txt` includes the API for local development.

Build the container with `docker build -t tool-transformer-split-rows .`.
