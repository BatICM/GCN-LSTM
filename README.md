Battery SOH Estimation Using GCN-LSTM

This project implements a Graph Convolutional Network (GCN) combined with a Long Short-Term Memory (LSTM) network to estimate the State of Health (SOH) of lithium-ion batteries.
The model leverages time-series voltage data from charge cycles, converting them into graph structures for deep learning–based regression.

📘 Overview

The pipeline performs the following steps:

Data Loading

Reads .mat battery datasets (MATLAB format).

Extracts charging cycle data: Voltage (V), Capacity (C), Charge quantity (Q), and Time (T).

Data Cleaning and Preprocessing

Sorts and filters data.

Aligns charge cycles around a current switch point (Q_0).

Performs linear interpolation on voltage-time curves.

Graph Construction

Splits interpolated voltage sequences into node segments.

Generates edge connections and weights using inner-product similarity.

Creates PyTorch Geometric Data objects for each cycle.

Model Architecture

Two GCN layers extract topological and feature relationships.

LSTM layer captures temporal dependencies across nodes.

A fully connected layer predicts the battery SOH.

Training and Evaluation

Uses a custom MAE (Mean Absolute Error) loss function.

Optimized with Adam and a step learning rate scheduler.

Trained for 100 epochs and tested on unseen cycles.

Visualization

Plots predicted vs. actual SOH curves.

Displays error distribution histogram and regression scatter plots.

⚙️ Dependencies

Install the required packages before running:

pip install numpy matplotlib scipy scikit-learn torch torch-geometric


⚠️ Note:
Ensure that your version of torch-geometric matches your installed torch version.
Example:

pip install torch==2.2.0 torch-geometric==2.4.0

🗂️ Data Preparation

The input file should be a MATLAB .mat file containing battery cycle data structured as:

batchX[number][2][0][i][1] → time array
batchX[number][2][0][i][2] → charge quantity
batchX[number][2][0][i][3] → current
batchX[number][2][0][i][4] → voltage
batchX[number][2][0][i][8] → capacity


Update the following parameters in the script:

root = 'D:/data/data_new/matlab_data1_21_48.mat'  # path to .mat file
fl = loadmat(root)['batch4']                      # dataset name
number = 7                                        # cell index
singal_size = 10                                  # node length
Initial_capacity = 1.1                            # reference capacity
Q_0 = Initial_capacity * 0.27                     # SOC switching point

🧠 Model Details
Architecture
Layer	Type	Output Dim	Activation
1	GCNConv	80	ReLU
2	GCNConv	40	ReLU
3	LSTM	10	—
4	Linear	1	—
🚀 Training

Run the training pipeline:

python main.py


The model will:

Train for 100 epochs

Print training loss after each epoch

Save the best model as model.pth under models/

🧩 Evaluation Metrics

MAE (Mean Absolute Error)

RMSE (Root Mean Square Error)

These metrics evaluate prediction accuracy against real SOH values.

📊 Visualization

Two main plots are generated:

Cycle vs. SOH Comparison

Actual vs. Predicted SOH values per cycle.

Error Distribution

Scatter plot of observed vs. estimated SOH.

Embedded histogram showing error distribution.

📁 Outputs
File	Description
model.pth	Trained model weights
plots/	Folder for visualizations
logs.txt	Training progress log (optional)
