# Configuring rsync for Deployment Synchronization

Deployment synchronization can be done using
[rsync](https://download.samba.org/pub/rsync/rsync.html), which is a
file copying tool. These changes must be done in the manager node and in
the same directory.

1.  Create a file called `           workers-list.txt          ` that
    lists all the worker nodes in the deployment. The following is a
    sample of the file where there are two worker nodes.

    !!! tip
    
        **Tip** : Different nodes are separated by new lines.
    

    **workers-list.txt**

    ``` java
    ubuntu@192.168.1.1:~/setup/192.168.1.1/as/as_worker/repository/deployment/server
    ubuntu@192.168.1.2:~/setup/192.168.1.2/as/as_worker/repository/deployment/server
    ```

2.  Create a file to synchronize the
    `           <PRODUCT_HOME>/repository/deployment/server          `
    folders between the manager and all worker nodes.

    !!! note
    
        **Note** : You must create your own SSH key and define it as the
        `           pem_file          ` . Alternatively, you can use an
        existing SSH key. Specify the
        `           manager_server_dir          ` depending on the location
        in your local machine. Change the logs.txt file path and the lock
        location based on where they are located in your machine.
    

    **rsync-for-carbon-depsync.sh**

    ``` java
    #!/bin/sh

    manager_server_dir=~/wso2as-5.2.1/repository/deployment/server/
    pem_file=~/.ssh/carbon-440-test.pem


    #delete the lock on exit
    trap 'rm -rf /var/lock/depsync-lock' EXIT 

    mkdir /tmp/carbon-rsync-logs/


    #keep a lock to stop parallel runs
    if mkdir /var/lock/depsync-lock; then
      echo "Locking succeeded" >&2
    else
      echo "Lock failed - exit" >&2
      exit 1
    fi


    #get the workers-list.txt
    pushd `dirname $0` > /dev/null
    SCRIPTPATH=`pwd`
    popd > /dev/null
    echo $SCRIPTPATH


    for x in `cat ${SCRIPTPATH}/workers-list.txt`
    do
    echo ================================================== >> /tmp/carbon-rsync-logs/logs.txt;
    echo Syncing $x;
    rsync --delete -arve "ssh -i  $pem_file -o StrictHostKeyChecking=no" $manager_server_dir $x >> /tmp/carbon-rsync-logs/logs.txt
    echo ================================================== >> /tmp/carbon-rsync-logs/logs.txt;
    done
    ```

3.  Create a Cron job that executes the above file every minute for
    deployment synchronization. Do this by running the following command
    in your command line.

    !!! note
    
        **Note** : You can run the Cron job on one given node (master) at a
        given time. If you switch it to another node, you must stop the Cron
        job on the existing node and start a new Cron job on the new node
        after updating it with the latest files so far .
    

    ``` java
    *   *  *   *   *     /home/ubuntu/setup/rsync-for-depsync/rsync-for-depsync.sh
    ```
