#python #logging #logs

```python

## Basic setup
import logging

LOGS_ERRORS_PATH = path / "pipeline_logs" / "errors" 
file_name = LOGS_ERRORS_PATH / "nans_in_unzipped_results_csv.log"

logging.basicConfig(level=logging.DEBUG, filename=file_name, filemode='a+', format='%(name)s - %(levelname)s - %(message)s - %(stack_info)s')
logging.debug('This will get logged')

## If logging doesn't save to a file, add this at the top of your script.
## Source: https://stackoverflow.com/a/51843801

for handler in logging.root.handlers[:]:
    logging.root.removeHandler(handler)

```
