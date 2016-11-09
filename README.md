# node_test

# more comments

# last comments

# one more


(function(){

    var rec = new GlideRecord('u_in_transit_cartons');
    rec.addEncodedQuery('u_receiving_storeSTARTSWITH35219^u_status!=auto_closed^ORu_status=NULL');
    rec.query();

    var cart;
    while(rec.next()){
        gs.addInfoMessage(rec.getValue('u_carton_id'));
        cart = new GlideRecord('x_kasp_orphaned_tr_confirmed_cartons');
        cart.setValue('carton_id', rec.getValue('u_carton_id'));
        cart.setValue('to_site','35219');
        cart.setValue('ticket','35219');
        cart.setValue('in_transit_type', rec.getValue('u_in_transit_type'));
        cart.insert();
    }
})();