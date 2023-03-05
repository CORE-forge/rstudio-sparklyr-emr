# Installing R, R Studio, and Hadoop on EMR machines

This script installs R, R Studio, and Hadoop on EMR machines. It compiles R from source and installs it to `/usr/local/`. It also installs and starts R Studio on the main node of the EMR cluster. Finally, it installs some common R packages that are used in a blog example.

## Usage

1. Copy and paste the script into a text file, then save the file with a `.sh` extension (e.g. `install_r_studio_hadoop.sh`).
2. Make the script executable with the command `chmod +x install_r_studio_hadoop.sh`.
3. Run the script with the command `./install_r_studio_hadoop.sh`.

## Explanation of the script's commands

- `set -x -e`: Enables debugging (`-x`) and causes the script to exit immediately if any command fails (`-e`).
- `rver=4.0.3`: Sets the desired version of R.
- `rspkg=rstudio-server-rhel-1.3.1093-x86_64.rpm`: Sets the R Studio package that will be downloaded.
- `rspasswd=hadoop`: Sets the password for the R Studio user `hadoop`.
- The `grep` command checks whether we're running on the main node.
- The `yum install` command installs some additional R and R package dependencies.
- The `mkdir` and `cd` commands create and enter the `/tmp/R-build` directory.
- The `curl` command downloads the R source code.
- The `tar` command extracts the R source code.
- The `./configure` command configures the R installation.
- The `make` command builds R.
- The `sudo make install` command installs R.
- The `cat` command creates a temporary file with R environment variables for EMR.
- The `cat` and `sudo tee -a` commands add the environment variables to `/usr/local/lib64/R/etc/Renviron`.
- The `sudo /usr/local/bin/R CMD javareconf` command reconfigures Java support before installing packages.
- The `curl` command downloads the R Studio package.
- The `sudo mkdir -p` command creates the `/etc/rstudio` directory.
- The `sudo sh -c` command adds an `auth-minimum-user-id` setting to the `rserver.conf` file.
- The `sudo yum install` command installs R Studio.
- The `sudo rstudio-server start` command starts R Studio (only on the main node).
- The `sudo sh -c` command sets the password for the `hadoop` user.
- The `sudo /usr/local/bin/R --no-save` command installs some common R packages.
