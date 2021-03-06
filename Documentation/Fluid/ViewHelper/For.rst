.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt

f:for
=====

The f:for ViewHelper is THE ViewHelper for generating lists. Take a look at the extensive examples.

Properties
----------

.. t3-field-list-table::
 :header-rows: 1

 - :Property,20:    Property
   :Datatype,20:    Variable type
   :Description,40: Description
   :Standard,10:    Standard
   :Mandatory,10:   Mandatory

 - :Property:    each
   :Datatype:    Array
   :Description: The array or object to be iterated
   :Standard:    NULL
   :Mandatory:   Yes

 - :Property:    as
   :Datatype:    String
   :Description: The name of the variable which contains the values of the current loop iteration
   :Standard:    NULL
   :Mandatory:   Yes

 - :Property:    key
   :Datatype:    String
   :Description: If you need the key of the current loop iteration, this is the name of the variable containing it.
   :Standard:    Empty string
   :Mandatory:   Yes

 - :Property:    reverse
   :Datatype:    Boolean
   :Description: The loop will backwards
   :Standard:    FALSE
   :Mandatory:   Yes

 - :Property:    iteration
   :Datatype:    String
   :Description: An array variable related to the current iteration, which identifies whether it is in the first or 
                 last loop index. This variable also contains values for index, cycle, total, isEven and isOdd
   :Standard:    NULL
   :Mandatory:   Yes

Simple example
--------------

::

 <f:alias map="{employees: {0: {first_name: 'Stefan', city: 'Lindlar'},1: {first_name: 'Petra', city: 'Lindlar'},2: {first_name: 'Sascha', city: 'Remscheid'},3: {first_name: 'Patrick', city: 'Bonn'},4: {first_name: 'Sven', city: 'Gummersbach'},5: {first_name: 'Andrea', city: 'Wuppertal'}}}">
   <table cellpadding="5" cellspacing="0" border="2">
     <f:for each="{employees}" as="employee">
       <tr>
         <td>{employee.first_name}</td>
         <td>{employee.city}</td>
       </tr>
     </f:for>
   </table>
 </f:alias>

This creates a new table row for each of the entries in the 'employee' array.

Example for reverse iteration
-----------------------------

::

 <f:alias map="{employees: {0: {first_name: 'Stefan', city: 'Lindlar'},1: {first_name: 'Petra', city: 'Lindlar'},2: {first_name: 'Sascha', city: 'Remscheid'},3: {first_name: 'Patrick', city: 'Bonn'},4: {first_name: 'Sven', city: 'Gummersbach'},5: {first_name: 'Andrea', city: 'Wuppertal'}}}">
   <table cellpadding="5" cellspacing="0" border="2">
     <f:for each="{employees}" as="employee" reverse="1">
       <tr>
         <td>{employee.first_name}</td>
         <td>{employee.city}</td>
       </tr>
     </f:for>
   </table>
 </f:alias>

The parameter 'reverse' may alternatively contain TRUE instead of 1.

Example with key variable
-------------------------

::

 <f:alias map="{employees: {0: {first_name: 'Stefan', city: 'Lindlar'},1: {first_name: 'Petra', city: 'Lindlar'},2: {first_name: 'Sascha', city: 'Remscheid'},3: {first_name: 'Patrick', city: 'Bonn'},4: {first_name: 'Sven', city: 'Gummersbach'},5: {first_name: 'Andrea', city: 'Wuppertal'}}}">
   <table cellpadding="5" cellspacing="0" border="2">
     <f:for each="{employees}" as="employee" key="entrynumber">
       <tr>
         <th colspan="2">Eintrag: {entrynumber}</th>
       </tr>
       <tr>
         <td>{employee.first_name}</td>
         <td>{employee.city}</td>
       </tr>
     </f:for>
   </table>
 </f:alias>

Example with iterator information
---------------------------------

::

 <f:alias map="{employees: {0: {first_name: 'Stefan', city: 'Lindlar'},1: {first_name: 'Petra', city: 'Lindlar'},2: {first_name: 'Sascha', city: 'Remscheid'},3: {first_name: 'Patrick', city: 'Bonn'},4: {first_name: 'Sven', city: 'Gummersbach'},5: {first_name: 'Andrea', city: 'Wuppertal'}}}">
   <table cellpadding="5" cellspacing="0" border="2">
     <f:for each="{employees}" as="employee" iteration="iterator">
       <f:if condition="{iterator.isFirst}">
         <tr>
           <th colspan="2">List of employees</th>
         </tr>
       </f:if>
       <tr>
         <td>Iteration beginning with 0: {iterator.index}</td>
         <td>Iteration beginning with 1: {iterator.cycle}</td>
         <td{f:if(condition:iterator.isOdd, then: ' style="color: green;"')}>{employee.first_name}</td>
         <td{f:if(condition:iterator.isEven, then: ' style="color: red;"')}>{employee.city}</td>
       </tr>
       <f:if condition="{iterator.isLast}">
         <tr>
           <th colspan="2">Number of employees: {iterator.total}</th>
         </tr>
       </f:if>
     </f:for>
   </table>
 </f:alias>

iterator.cycle is - just like iterator.index - simply a counter. It has nothing to do with the separate ViewHelper 
f:cycle.