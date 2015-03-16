build: 
  sudo docker build -t jeffmt/ensime .

run: 
  sudo docker run -t -i jeffmt/ensime /bin/bash

run  with persistent data volume:
  sudo docker run -t -i --volumes-from=<data volume container name> jeffmt/ensime /bin/bash

