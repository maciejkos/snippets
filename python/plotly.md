How to combine plotly express plots? #plotly #python #plots #px
```python
fig_1 = px.line(x = periods, y = work_remaining_history)
fig_2 = px.line(x = periods, y = task_queue_completion_history)

fig_1.add_traces(
    list(fig_2.select_traces())
)
fig_1

# THE BELOW WORKS BETTER B/C YOU HAVE EASIER CONTROL OVER INDIVIDUAL TRACES

newnames = {'wide_variable_0':'work_remaining_history', 
            'wide_variable_1': 'task_queue_completion_history', 
            'wide_variable_2': 'capacity_history'}
fig_1 = px.line(x = periods, y = [work_remaining_history, task_queue_completion_history, capacity_history], title = "Work Remaining").update_layout(showlegend=True)

fig_1.for_each_trace(lambda t: t.update(name = newnames[t.name],
                                      legendgroup = newnames[t.name],
                                      hovertemplate = t.hovertemplate.replace(t.name, newnames[t.name])
                                     ))

```