# Glossary

## Application

An Application is Lucee is any code running within the context of a single Application.cfc. Usually there is one Application.cfc per website, and thus one application, however it is possible to have multiple Application.cfc's per website. 

## guard assertion

A check at the beginning of the function that some condition occurs, otherwise throw an error.

## Mapping

A setting in the Application.cfc that tells Lucee how to include templates and into import components

## Request Scope

A variable Scope which only exists for the life of a single HTTP request. Once the request is finished, Lucee deletes the variables. 

## Tags

A Tag is a primary part of the Lucee language and allows for building output in Templates.

## Templates

Lucee files with the extension .cfm which are used to render HTML and other output

## User Defined Functions

Functions written in Lucee which are not closures. 

## isomorphic javascript

An application in which the views can be rendered server side or in javascript. This speeds up the initial page load and subsequent changes can replace fragments of the page.