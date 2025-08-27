# Lwc-Revision
Wire and ConnectedCallback
<template>
    <lightning-input 
        type="text" 
        variant="standard" 
        name="Put data" 
        label="label" 
        placeholder="type here..." 
        onchange={handleChange}>
    </lightning-input>

    {showData}
</template>
# LWC JS

js

import { LightningElement, wire } from 'lwc';
import callingWire from '@salesforce/apex/wireAndImperativeController.getAccount';

export default class WireAndImperative extends LightningElement {
    myname = 'New';
    showData;

    // Using Wire
    @wire(callingWire, { name: '$myname' })
    wiredData({ error, data }) {
        if (data) {
            this.showData = data.Name;
        } else if (error) {
            console.error('Error:', error);
        }
    }

    handleChange(event) {
        this.myname = event.target.value;
    }

    // Using ConnectedCallback with imperative call
    /*
    connectedCallback() {
        callingWire({ name: this.myname })
            .then((result) => {
                this.showData = result.Name;
            })
            .catch((error) => {
                console.error('Error:', error);
            });
    }
    */
}
Apex Controller
apex

public class wireAndImperativeController {
    @AuraEnabled(cacheable=true)
    public static Account getAccount(String name) {
        return [SELECT Id, Name FROM Account WHERE Name = :name LIMIT 1];
    }
}



https://medium.com/@kashishbansal1798/parent-child-communication-in-lwc-251b75ea4515
https://www.youtube.com/watch?v=wRdCT4WMER0



 Decorators - @api , @track , @wire | With Most Practical Examples
