# Dockerfile

# Use the official Jupyter Notebook base image
FROM jupyter/base-notebook:latest

# Set environment variables for Jupyter
ENV JUPYTER_ENABLE_LAB=yes

# Expose the default Jupyter port
EXPOSE 8888

# Optionally, install additional Python packages
RUN pip install --no-cache-dir \
    numpy \
    pandas \
    matplotlib \
    scikit-learn 

# Set the command to start Jupyter Notebook
CMD ["start-notebook.sh"]