# soccer app

> A simple setup of a backend server setup in node.js serving soccer data from a local csv-file to a single page frontend app in Vue. The server provides a REST API allowing for:


* Retreiving a list of players
* Retrieving statistics for a selected player
 

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

> The server setup should be cloned from [this repository](https://github.com/bjabu/frontendtest-node). Both server and client servers should be started.


### Comments
* I did choose **Vue** as it is convenient for small seetups and I have a decent knowledge.
* Initial comments mentioned porting server to Java. I did choose to see that as a typo and kept **node.js** as it would at least have taken me a workday. I have not been close to Java coding for fifteen years (though I use the IntelliJ editor).
* **Limitations:**  No decent error handling. 
