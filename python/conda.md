```shell

# list existing environments
conda info --envs

# create a new env
# https://docs.conda.io/projects/conda/en/4.6.0/user-guide/tasks/manage-environments.html
conda create --name env_name

# remove env
conda remove --name env_name --all


# conda tab completion on Linux
# https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/enable-tab-completion.html
conda install argcomplete
eval "$(register-python-argcomplete conda)"

#########
# conda with powershell
## https://stackoverflow.com/a/67996662

## Open a `Anaconda Powershell Prompt` from Start Menu. Now Try:
conda init powershell
## now close powershell and open it as admin

## conda scripting with powershell

### just create a new env
### create file create_env.ps1 in, e.g., local git folder of your project, e.g., GitHub/my_project
### Usage .\create_env.ps1 -name keyboard_design -pyver 3.10

param(
    [Parameter(Mandatory=$true)][String]$name,  # the name of new env
    [String]$pyver = "3.6"
)

Invoke-Expression "conda create --name $name python=$pyver"
Invoke-Expression "conda activate $name"
Write-Host "Done. You are now at $name with the environment created following the parameters provided."

## create a new env and install python packages with conda and pip
# https://gist.github.com/sleepiejohn/445bcd61845d6bb178290ff7613318ee

### Usage: pyenv -name myenv -pyver 3.6 -conda pandas,numpy,scipy -pip tensorflow,matplotlib

### create file pyenv.ps1 in, e.g., local git folder of your project, e.g., GitHub/my_project

param(
    [Parameter(Mandatory=$true)][String]$name,  # the name of new env
    [String]$pyver = "3.6", # the python version defaults to 3.6
    [String[]]$pip, # comma separated list of packages to install with pip
    [String[]]$conda, # comma separated list of packages to install with conda
    [bool]$mkdir=$true # create a directory for the project
)

$condaPkgs = [system.String]::Join(" ",  $conda)
$pipPkgs   = [system.String]::Join(" ",  $pip)


Invoke-Expression "conda create --name $name python=$pyver $condaPkgs -y"
Invoke-Expression "conda activate $name"
Invoke-Expression "pip install $pipPkgs"
#if ($mkdir) {
#    mkdir $name
#    Set-Location $name
#}
#pip freeze > requirements.txt
Write-Host "Done. You are now at $name with the environment created following the parameters provided."


#################



```