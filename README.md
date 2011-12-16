ChiliProject on OpenShift
=========================
 
ChiliProject is a web based project management system. Written using Ruby on Rails framework, it is cross-platform and cross-database.

ChiliProject is open source and released under the terms of the GNU General Public License v2 (GPL).

More information can be found on the official ChiliProject set (www.chiliproject.org)
Running on OpenShift
--------------------

Create an account at http://openshift.redhat.com/

Create a rails application

	rhc-create-app -a chiliproject -t rack-1.1

Add mysql support to your application
    
	rhc-ctl-app -a chiliproject -e add-mysql-5.1
Make a note of the username, password, and host name as you will need to use these to login to the mysql database

Add this upstream rails quickstart repo

	cd chiliproject
	rm -rf *
	git remote add upstream -m master git://github.com/mastersin/chiliproject-openshift-quickstart.git
	git pull -s recursive -X theirs upstream master

Add your database username and password 

	vi config/database.yml
	git commit -a -m "Adding mysql auth information"

Then push the repo upstream

	git push

That's it, you can now checkout your application at:

	http://chiliproject-$yournamespace.rhcloud.com

Use the following to login to your new chiliproject application running on openshift

	username: admin
	password: admin

