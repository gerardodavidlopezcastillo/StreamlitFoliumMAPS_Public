# Use the base image of Python 3.9
FROM python:3.9

# streamlit-specific commands
# Create a directory for Streamlit configurations and create a credentials.toml file
RUN mkdir -p /root/.streamlit
RUN bash -c 'echo -e "\
[general]\n\
email = \"\"\n\
" > /root/.streamlit/credentials.toml' \
# Create a Streamlit configuration file (config.toml) with certain options
RUN bash -c 'echo -e "\
[server]\n\
enableCORS = false\n\
enableXsrfProtection=false\n\
" > /root/.streamlit/config.toml'

# Expose port 8501, which is the default port for Streamlit
EXPOSE 8501
# Copy all content from the current directory to the "app" directory in the container
COPY . ./app
# Install Python dependencies listed in the requirements.txt file
RUN pip3 --trusted-host=pypi.python.org --trusted-host=pypi.org --trusted-host=files.pythonhosted.org install -r app/requirements.txt

# Copy all content from the current directory to the container again
COPY . .

# Command to run the Streamlit application with custom options
CMD streamlit run app/app.py --server.enableCORS=false server.enableXsrfProtection=false --server.headless=true --global.developmentMode=false --server.port="8501"