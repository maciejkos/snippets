#python #serialization #pickle #dill

```python

def save_pickle(object_to_pickle, file_name: str = "", file_path="", append_datetime: int=1, use_dill: int=0):
    """Saves object to pickle file.

    Args:
        object_to_pickle ([type]): 
            What object do you want to save as a pickle?
        file_name (str, optional): 
            What do you want to name the saved file? Eg. "cookies.pickle". The .pickle file extension is added automatically if you forget about it. This cannot be overwritten.
            DO NOT include "____" (4 or more underscores) in the name to avoid breaking append_datetime (see below). If empty, defaults to object name and datetime, e.g., "cookies____03-16-21__23-59-59.pickle". Cannot be overwritten with append_datetime = 0.
        file_path (pathlib path, optional): 
            Where do you want to save the file? Expects a pathlib object. If empty, defaults to current workining directory using path = pathlib.Path.cwd().
        append_datetime (int, optional): 
            Do you want to append datetime to the end of the file name (%m-%d-%y__%H-%M-%S). Defaults to 1, i.e., appending datetime, e.g., "cookies____03-16-21__23-59-59.pickle". Datetime is always after "____". Note that with file_name empty, datetime will be appended automatically. If you leave file_name empty and set append_datetime = 1, the datetime will be appended only once. 
        [EXPERIMENTAL, NOT TESTED] use_dill (int, optional): 
            Do you want to use dill instead of pickle for saving the file? It can help if pickle can't serialize object. Defaults to 0, i.e., to using pickle.

    Returns:
        [pathlib path]: 
            Path of the saved file.
		-1:
			If error.
	Usage:
		import pathlib

		path = pathlib.Path.cwd()
		fp = path  / "python" / "playground"

		my_obj = [x for x in range(1, 10)]
		save_pickle(my_obj, file_name = "my_shiny_obj.pickle", file_path=fp, append_datetime=1, use_dill=0)
    """
    assert "____" not in file_name, "ERROR: The file_name you provided includes '____' (4 or more underscores). \n\tThis isn't allowed."
    import pathlib

    from datetime import datetime
    now = datetime.now()
    current_date = now.strftime("%m-%d-%y__%H-%M-%S") # 03-16-21__23-59-59

    if file_name == "":
        # Get the name of a reference (variable name) pointing to object_to_pickle.
        object_to_pickle_var_name = [k for k,v in locals().items() if v == object_to_pickle][0] # If there are two such names, it returns only the "first" one. Not clear if the order is random or not.
        file_name = f"{object_to_pickle_var_name}____{current_date}.pickle"
    
    elif file_name != "":
        file_name = file_name.split(".pickle")[0]
        file_name = f"{file_name}.pickle"

    else:
        print("Something went wrong with `file_name`")
        return -1
    
    if append_datetime == 1:
        if "____" in file_name: # datatime already appended to the file name
            pass
        elif "____" not in file_name:
            file_name.split(".pickle")[0]
            file_name =  f"{file_name}____{current_date}.pickle" 
        else:
            print("Something went wrong with `append_datetime`")
            return -1

    path = pathlib.Path.cwd()

    if file_path == "":
        f_path = path / f"{file_name}"

    elif file_path != "":
        f_path = file_path / f"{file_name}" 

    else:
        print("Something went wrong with `file_path`")
        return -1   

    if use_dill == 0:
        import pickle
        with open(f_path, 'wb') as f:
            pickle.dump(object_to_pickle, f)
            print(f"PICKLE: Object saved to: \n\t{f_path}")
    elif use_dill == 1:
        import dill
        with open(f_path, 'wb') as f:
            dill.dump(object_to_pickle, f)
            print(f"DILL: Object saved to: \n\t{f_path}")

    return f_path

my_obj = [x for x in range(1, 10)]

import pathlib

path = pathlib.Path.cwd()
fp = path  / "python" / "playground"

save_pickle(my_obj, file_name = "my_shiny_obj.pickle", file_path=fp, append_datetime=1, use_dill=0)

def load_pickle(file_path_name, use_dill: int=0):
    """Reads a pickle

    Args:
        file_path_name (pathlib path):
            Where which file do you want to laod? e.g., fp = path / "additional_model_selection" / "my_pickle.pickle"
        [EXPERIMENTAL, NOT TESTED] use_dill (int, optional): 
            Do you want to use dill instead of pickle for loading the file? It can help if pickle was created using dill. Defaults to 0, i.e., to using pickle.

    Returns:
        loaded file.

    Usage:

        ## first save the object
        fp = path  / "python" / "playground"
        my_obj = [x for x in range(1, 10)]

        saved_file_path_name = save_pickle(my_obj, file_name = "my_shiny_obj.pickle", file_path=fp, append_datetime=1, use_dill=0)

        ## now load it
        saved_file_path_name = pathlib.PurePath(saved_file_path_name)
        loaded_file = load_pickle(file_path_name="saved_file_path_name", use_dill=0)
       
    """
    if use_dill == 0:
        import pickle
        with open(file_path_name, 'rb') as f:
            loaded_file = pickle.load(f)
            print(f"PICKLE: Object loaded from: \n\t{file_path_name}")
            
    elif use_dill == 1:
        import dill
        with open(file_path_name, 'rb') as f:
            loaded_file = dill.load(f)
            print(f"DILL: Object loaded from: \n\t{file_path_name}")
    
    return loaded_file
```