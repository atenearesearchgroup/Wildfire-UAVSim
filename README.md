# Project overview

## Project descritpion

Wildfire-UAVSim is a customizable wildfire tracking simulator that enables
the evaluation of diverse adaptation strategies. Among its many configuration parameters, we can customize the forest area with different densities of vegetation, as well as fire and smoke dispersion patterns that are affected by factors such as wind, conforming different observability conditions. The configuration options of our simulator also allow to place a team of UAVs in charge of tracking the fire over the forest area. Wildfire-UAVSim provides a graphical web interface native from Mesa framework, executed by the simulator, in order to keep track of how the simulation evolves in time.

## Files structure

5 Python files compose the project structure, namely:

### `agents.py`

This python file holds the logic for managing elements such as Fire, Smoke, Wind and UAVs.

### `widlfire_model.py`

This python file holds the logic for managing the wildfire simulation, by utilizing elements from `agents.py` file.

### `main.py`

This python file allows to execute the wildfire simulation built in `widlfire_model.py` file.

### `common_fixed_variables.py`

This python file holds the variables used to set the simulation execution configurations.

### `Canvas_Grid_Visualization.py`

# Installation setup

In the following subsections, the installation process for executing the project will be explained.

## Installing Pycharm Community Edition IDE

First, downloading and installing Pycharm Community Edition IDE is explained to easily run and set up the project and its dependencies.
Since this project is tested on Ubuntu 22.04.2 LTS, the user can use `snap` command in cmd (pre-installed from Ubuntu 16.04 LTS and later) as a fast installation option. The user must execute the command
`sudo snap install pycharm-community --classic` in cmd for installing Pycharm Community Edition.

As mentioned, this project was tested on Ubuntu 22.04.2 LTS, so for other OS were not. For checking system requirements, and information about the installation process for other OS,
visit https://www.jetbrains.com/help/pycharm/installation-guide.html.

## Opening the project

First extract the Wildfire-UAVSim downloaded package in any folder. Second, open Pycharm by executing the command `pycharm-community` in cmd, or searching for the executable in the computer.
Then, the projects window should be opened. Next, the user has to click on `Open`, select the extracted project folder, and click `OK`. A window should appear to select between light editor, and project editor.
Select project editor. For openning the project next tiems, repeat same process.

## Installing dependencies

Once the project is opened, some dependencies are necessary. To install them, first go to `Settings > Project > Python Interpreter`, then select the desired Python interpreter
for executing the project. As default `/usr/bin/python3.10` should appear in the `Python Interpreter:` tab, which already contain some default dependencies if Ubuntu 22.04.2 LTS is installed. For other Python interpreters,
other dependencies may be needed to be installed. On the same Pycharm configuration window, click on `+` icon, and search for the following dependencies (selecting the version should be done for testing project same way as
it was done for the research paper. It can be done with the `Specify version` checkbox):

<ul>
  <li>Mesa (v.1.2.1)</li>
  <li>numpy (v1.24.2)</li>
  <li>matplotlib (v3.7.1)</li>
</ul>

## Execution of the project

Once project is opened, and dependencies were installed, `main.py` can be executed by selecting the file, right mouse click, and clicking on `Run 'main'` (shortcut should be `Ctrl+Mayus+F10`).
A web page interface should appear, with the wildfire grid, and buttons for configuring the simulation.

# Graphical interface functionalities

When executing the project as explained above, a web page hosted in http://127.0.0.1:8521/ should appear in user's default browser. Port can be modified in `main.py` file if user has that the default one already busy. The graphical interface should look like:

![webpagegraphicalinterfaceelements](https://github.com/envilk/Wildfire-UAVSim/assets/25938116/a230ebb9-0db6-491e-abd8-b0edec127a95)

The relevant graphical interface elements are:

### `Grid`

The grid with generated cells, with vegetation, fire, smoke, and UAVs, can be seen in the center of the screen.

### `Start button`

The start button allows to run the simulation without stopping.

### `Step button`

The step button allows to execute one time step at a time.

### `Reset button`

The reset button allows to execute the `reset()` method, inherited and overwritten from Mesa framework class `mesa.Model`, into WildFireModel class, inside `widlfire_model.py` file.

### `Frames per second`

Is a slider that allows to set the frames per second (FPS) velocity for the graphical visualization of the simulation execution. Each frame corresponds to one time step. Its range goes from 1 to 20 FPS, taking into account that, counterintuitively, 0 FPS set the fastest FPS velocity. If sometimes the simulation seems that is not working fluetnly, it may be caused by the `FIRE_SPREAD_SPEED` variable referenced below.

### `Current step counter`

Indicates the current time step of the simulation.

# Common variables configuration

Global variables are used in the project to configure different simulation executions. In the next subsections several global variables descriptions are shown, as well as many configuration examples for execution.

## Variables description

### Forest area

`BATCH_SIZE`: Establishes how long the simulation will run, in number of time steps.

`WIDTH`, `HEIGHT`: Set the grid size (forest area size) in cells.

`BURNING_RATE`: Sets the fuel decay speed in terms of time steps.

`FIRE_SPREAD_SPEED`: Sets how fast fire spreads to other cells, in terms of time steps.

`FUEL_UPPER_LIMIT`, `FUEL_BOTTOM_LIMIT`: Establish the maximum and
minimum amount of burnable fuel present in each cell, respectively.

`DENSITY_PROB`: Is a value in the range `[0, 1]` that establishes the
percentage of the grid covered by vegetation.

### Wind

`ACTIVATE_WIND`: Sets whether the fire spread is influenced by wind.

`FIXED_WIND`: If is active, then wind blows in the direction set by `WIND_DIRECTION`. If it is not, it means wind blows two directions, specified by `FIRST_DIR` and `SECOND_DIR`. Since wind can blow a direction stronger than the
other one, `FIRST_DIR_PROB` establishes the wind first direction’s predominance.

`PROBABILITY_MAP`: If is active, the probability of the fire to spread to each cell at all times can be visualized.

`MU`: Sets how strong wind blows with a value in the range `[0, 1]`.

### Smoke

`ACTIVATE_SMOKE`: Sets whether smoke will be part of the simulation.

`SMOKE_PRE_DISPELLING_COUNTER`: Establishes how fast smoke appears after fire starts in a cell.

### UAV

`NUM_AGENTS`: Establishes the amount of UAVs that will fly over the forest area (zero indicates the simulator will simulate only the wildfire spread).

`N_ACTIONS`: Specifies the number of possible actions each UAV can take when deciding on a move, which we set as `[north, east, west, south]`.

`UAV_OBSERVATION_RADIUS`: Sets the observation radius—technically it is not really a radius, since observed areas have square shapes.

`SECURITY_DISTANCE`: Establishes the minimum distance that UAVs should be separated from each other for avoiding collisions.

## Configuration examples

Three default examples of how different variables can be configured to develop distinct scenarios, can be seen below.
