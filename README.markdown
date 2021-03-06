# CakePHP Backbone Js Plugin

Load Backbone.js files and bootstrap your models with ease.

## Background

Easily enforce structure with your backbone.js app without having to toil over managing your included javascript. Bootstrap models in the correct backbone.js format with common, helpful options.

This was built for my personal projects so if it doesn't meet your needs make issues or submit patch requests. The API will probably change (improve!) once it's being used on a few more projects.

## Requirements

* PHP >= 5.3 (5.2 could work if you remove visibiltiy from vars and methods)
* CakePHP 2.x
* Backbone.js (not included)
* Backbone forms if you want: https://github.com/powmedia/backbone-forms
* A minimal understanding of helpers, plugins, and backbone.js so you can debug if anything goes wrong.

## Installation

_[Manual]_

* Download this: http://github.com/dkullmann/CakePHP-Backbone-Js-Helper/zipball/master
* Unzip that download.
* Copy the resulting folder to app/plugins
* Rename the folder you just copied to @[PLUGIN_NAME]@

_[GIT Submodule]_

In your app directory type:

	git submodule add git://github.com/dkullmann/CakePHP-Backbone-Js-Helper.git Plugin/Backbone
	git submodule init
	git submodule update

_[GIT Clone]_

In your plugin directory type

	git clone git://github.com/dkullmann/CakePHP-Backbone-Js-Helper.git Plugin/Backbone

### Enable plugin

In 2.0 you need to enable the plugin your `app/Config/bootstrap.php` file:

	CakePlugin::load('Backbone');

If you are already using `CakePlugin::loadAll();`, then this is not necessary.

## Usage

_Controller_

	public $helpers = array('Backbone.Backbone');

_View_

	# Files will be added to $scripts_for_layout, not inline
	$this->Backbone->init(
		array('Model' => 'UserModel'), // Load a single file
		array('View' => array('UserView', 'UserIndexView')), // Load many files
		);

	# Bootstrap a model
	echo $this->Backbone->bootstrap($user, 'User'); // Takes Model::find() results and formats them nicely

_More complex bootstrap_

	# Create var customName = { attributes };
	echo $this->Backbone->bootstrap($user, 'User', array('varName' => 'customName'));
	
	# Maybe we don't have an alias set in our variable (like CakePHP 2.x $this->Auth->user())
	echo $this->Backbone->bootstrap($user, null, array('varName' => 'User'));
	
	# Or maybe we want to merge other models we got with $contain in Model::find()
	echo $this->Backbone->bootstrap($user, 'User', array('merge' => 'Profile'));

## Options

* variable : _default: null_ The PHP view variable to bootstrap
* alias : _default: null_ The alias of the model you are bootstrapping, or null if there is no model
* options : _default: array()_ Array of options: 
    * inline : _default: false_ Set to true to echo the javascript inline, otherwise it's added to the pages $scripts_for_layout 
    * varName : _default: false_ Override the default name of the js variable produced. Defaults to the $alias parameter (req'd if $alias is null)
    * merge: _default: false_ Allows you to merge another alias from $variable into the javascript results, useful for hasOne and hasMany type relationships

## Todo

* Have more people use it and tell me what they want / patch it
* Potentially make it work nicely with AssetCompress so you aren't loading a zillion files from BackboneHelper::init()

## License

Copyright (c) 2012 David Kullmann

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.	