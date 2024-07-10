digraph ZHO_Web_App_Architecture {

rankdir=LR;

subgraph user {
    node [shape=box, color=lightblue];
    browser [label="Web Browser"];
}

subgraph app {
    node [shape=box, color=lightgreen];
    web_app [label="Web Application (Front-End)"];
    api_gateway [label="API Gateway"];
    auth_service [label="Authentication Service"];
    
    user -> web_app;
    web_app -> api_gateway;
}

subgraph services {
    node [shape=box, color=yellow];
    ms_user [label="User Mgmt. Service"];
    ms_onboarding [label="Onboarding Service"];
    ms_dashboard [label="Dashboard & Analytics Service"];
    ms_communication [label="Communication Service"];
    ms_resume [label="Resume Automation & Assessment Service"];
    ms_procurement [label="Procurement Service"];
    ms_finance [label="Finance Management Service"];
    ms_compliance [label="Compliance Service"];
    
    api_gateway -> {ms_user; ms_onboarding; ms_dashboard; ms_communication; ms_resume; ms_procurement; ms_finance; ms_compliance};
}

subgraph data {
    node [shape=ellipse, color=pink];
    db_main [label="Database (RDBMS)"];
    db_other [label="Database (NoSQL)"];
    
    {ms_user; ms_onboarding; ms_dashboard; ms_communication; ms_finance; ms_compliance} -> db_main;
    ms_resume -> db_other;  /* Optional: Resume data might benefit from NoSQL flexibility */
}

subgraph external {
    node [shape=box, color=lightgray];
    ext_tamkeen [label="Tamkeen Portal"];
    ext_payroll [label="Payroll System"];
    ext_uaecip [label="UAEICP (Optional)"];
    
    {ms_procurement; ms_finance} -> {ext_tamkeen [style=dashed]};
    ms_finance -> ext_payroll [style=dashed];
}

subgraph cloud {
    node [shape=box, color=skyblue];
    cloud_infra [label="Cloud Infrastructure Services"];
    
    {user; app; services; data; external} -> cloud_infra;
}

}
