from eclipse/dotnet_core

run sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \ 
  echo "deb https://download.mono-project.com/repo/ubuntu stable-xenial main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list && \
  sudo apt-get update && \
  sudo apt-get install mono-complete -y && \
  sudo apt-get -y clean && \
  sudo rm -rf /var/lib/apt/lists/*
