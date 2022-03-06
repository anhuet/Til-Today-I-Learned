## Setup SSH key

#### Generating a new SSH key
> $ ssh-keygen -t ed25519 -C "your_email@example.com"

#### Adding a new SSH key to  GitHub
> $ pbcopy < ~/.ssh/id_file.pub  
> Copies the contents of the id_ed25519.pub file to your clipboard  
Github -> Settings -> Add new SSH key
