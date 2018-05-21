---
layout: post
title: "Python, SQLite"
meta: "distributed-computing"
permalink: /case-studies/distributed-computing/
next-case-study-title: "000"
next-case-study-url: /case-studies/000/
hide-hire-me-link: true
---

<a href="/_post_images/2015/11/distributed.png"><img src="/_post_images/2015/11/distributed.png" alt="distributed" width="711" height="403" class="aligncenter size-full wp-image-6281" /></a>

Certain branches of research require many simulations of similar problems, differing through a series of parameters.  These parameters are typically given as fixed set of parameters or as random variables with mean value and standard variation.  With multiple computers available, I created a client-server tool that helped to parallelize and thus speed up those computations.

Note: In this instance the server was running of my laptop, with a client 'farm' hosted in a PC room at the University of Washington.

<strong>ARTEFACTS</strong>
- CreateDatabase.py
- GetProblem.py
- SubmitAnswer.py
- CheckResult.py
- JobManager.py
- Client.py
- documentation.pdf

<strong>DESCRIPTION</strong> 
This project was made entirely in Python (with the exception of some front-end HTML). It consisted of two parts, a server and a client. 
- Client applications are 'workers', installed on the available computers and running the calculations for an assigned set of parameters. After a calculation is done they communicate the result back to the server.
- The server application keeps track of which sets of parameters have been assigned, which are still to be assigned, what the results were and keeps an eye on possible time-out problems. It also presents a human user with a nice data visualization showing the received results. It stores parameter sets and results in a local database (SQlite).

<strong>DETAILS</strong>

<strong>The server...</strong>
- Communicates with clients through a request function that responds to a HTTP-request: <a href="http://server_name/GetProblem.py?UID=uid?JOB=new">http://server_name/GetProblem.py?UID=uid?JOB=new</a> by returning “{‘jobID’:jid, ‘param1’:val1, ‘param2’:val2, … }” through the web interface (visible in browser). 

- Keeps track of which user works on what combination (through the database). Generates a new user if uid is not yet known.  Also keep track when a job was assigned and have the problem expire/reset if no solution is submitted within a given time (1 minute).

- Generates a request function that responds to a HTTP request (<a href="http://server_name/SubmitAnswer.py?UID=uid?JOB=jid?result=val">http://server_name/SubmitAnswer.py?UID=uid?JOB=jid?result=val</a>)
that 
- checks for valid uid and active jid
- registers the result and stores it within the combinations table (SQL UPDATE statement)
- marks the problem as completed
- returns ‘TRUE’ if action was successful and ‘FALSE’ if a problem was encounters. Add proper description of the problem in a separate line of output (will be displayed over the HTTP connection.

- Generate a request function that responds to a HTTP request (<a href="http://server_name/CheckResult.py">http://server_name/CheckResult.py</a>)
that shows a human:
- a distribution graph for the submitted values (density function)
- presents mean, std dev, and COV for the computed results.  
- Lists all contributing users and how many computations they submitted.

<strong>The client...</strong>
- Obtains a new set of input parameters by submitting the following request via a HTTP connection: <a href="http://server_name/GetProblem.py?UID=uid?JOB=new">http://server_name/GetProblem.py?UID=uid?JOB=new</a> where uid is your personal ID.

- Uses these parameters to solve a statistical problem. It returns the solution through an HTTP request:
<a href="http://server_name/SubmitAnswer.py?UID=uid?JOB=jid?result=X">http://server_name/SubmitAnswer.py?UID=uid?JOB=jid?result=X</a> 
The server then returns ‘TRUE’ (if action was successful) or ‘FALSE’ (if a problem was encounters, along with a line describing the problem).

<strong>DATABASE</strong>
<a href="/_post_images/2015/11/Screenshot-2015-11-07-13.42.48.png"><img src="/_post_images/2015/11/Screenshot-2015-11-07-13.42.48.png" alt="Screenshot 2015-11-07 13.42.48" width="697" height="401" class="aligncenter size-full wp-image-6288" /></a>

<strong>CODEFRAGMENT PYTHON 'GetProblem.py'</strong>
--
<code>
    #!/usr/bin/python

    import cgi
    import sys

    print("Content-Type: text/html\n") #Required to prevent internal server error

    import cgitb
    cgitb.enable()#output error to client window 
    from job_manager import *
     
    def main():
        final_feedback='Summary for job request:\n'
        form = cgi.FieldStorage()
        manager=job_manager('./table.db')
     
        # set name or use default name if no name was provided
        if form.has_key("username"): 
            username = form.getvalue('username')
            final_feedback+='Server received username: {}.\n'.format(username)
        else:
            username = 'Empty'
            final_feedback+='The Client did not specify a username. The server made it as default: "Empty".\n'
        final_feedback +='Username:{}\n'.format(username)

        userid=manager.register_user(username) #if the username exist in database, it will return user.id, or it will create a new user.id and return that
        print "ID of the client is {}".format(userid)
        final_feedback += 'ID of the client: {}.\n'.format(userid)

        print "Looking for new problem to solve..."
        parameterid=manager.get_new_parameterid()
        
        if parameterid == None: #If the get_new_parameterid() function return None, there is no problem to be solved. program exists.
            print "There is no problem to be solved."
            print final_feedback
            sys.exit()
        else:
            print "Find one! The ID of the problem is {}".format(parameterid)

        final_feedback += 'ID of the assigned problem is {}.\n'.format(parameterid)

        #The sentence below assigns a specific problem to a client with a specific userid
        parameters=manager.assign_a_job(userid,parameterid)#This will print a dict of parameters
        print "The parameters for this problem are?{}?{}?{}?{}?{}".format(parameters[0],parameters[1],parameters[2],parameters[3],parameters[4])
        print "Waiting for result from client..."
        print final_feedback 
  
    main()
</code>
--

---

{% include promo-next.html %}
