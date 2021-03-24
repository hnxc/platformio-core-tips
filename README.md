# platformio-core-tips

If you want to add date time of compilation like this

```bash
========= [SUCCESS] Took 24.32 seconds at __ 24/03/2021 11:04:25 __  =========
```

Open file at `C:\Users\xxxxx\.platformio\penv\Lib\site-packages\platformio\commands\run\command.py`

Change the function (line 207)

```python
def print_processing_footer(result):
    from datetime import datetime
    # datetime object containing current date and time
    now = datetime.now()
    dt_string = now.strftime("%d/%m/%Y %H:%M:%S")
    is_failed = not result.get("succeeded")
    util.print_labeled_bar(
        "[%s] Took %.2f seconds at __ %s __ "
        % (
            (
                click.style("FAILED", fg="red", bold=True)
                if is_failed
                else click.style("SUCCESS", fg="green", bold=True)
            ),
            result["duration"],
            click.style(dt_string, fg="yellow", bold=True)
        ),
        is_error=is_failed,
    )
```
