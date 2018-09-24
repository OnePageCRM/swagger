#OnepageCRM API
<i>OnePageCRM converts the complexity of a CRM system to a simple to-do list. For more information on OnePageCRM please visit our [website](https://www.onepagecrm.com).</i><br><br>

###OpenAPI 3 Compliance
We've rebuilt the OnepageCRM's API documentation from the ground up to be cleaner, simpler and to comply with the <a target="_blank" href="https://github.com/OAI/OpenAPI-Specification">OpenAPI3 specification</a>. <br>
We are also releasing our OpenAPI 3 compliant documentation to the public: <a target="_blank" href="https://github.com/OnePageCRM/swagger">https://github.com/OnePageCRM/swagger</a>.<br>
If you think our docs could be clearer or notice any issues, please let us know. We would also be delighted to receive your pull requests. <br>
You can find a list of tools to work with OpenAPI <a href="http://openapi.tools/">here</a>. Feel free to use any and all of these tools with the the OnepageCRM spec. For example you could generate a client sdk for your favourite language or mock API responses.<br>
In rewriting this documentation we have exposed lots of new features of the API. We hope you enjoy using them! <br>

##Generate Client Libraries using openapi-generator
Openapi-generator is an open source tool that can be used to generate API client libraries (SDK generation). 

To generate a Ruby client library run the following 

    docker run --rm -v ${PWD}:/local openapitools/openapi-generator-cli generate \
    -i https://raw.githubusercontent.com/OnePageCRM/swagger/master/swagger.yaml \
    -g ruby \ 
    -o /local/client_libs/ruby \
    -c /local/codegen/ruby/ruby.conf \
    -t /local/codegen/ruby \ 
    --remove-operation-id-prefix

The above options specify the following:<br>
-i: The spec to generate from. To generate a client based on a local version of this file, supply a local file path to the OpenApi spec.  
-g: The language to generate<br>
-o: The output directory<br>
-c: Language specific config file<br>
-t: Language specific template file<br>

To generate a library in another language do the following: 
1) Create a config file under codegen/{language} called {language}.conf
2) Using your favourite editor, enter all nescorry config options. The config options for your language can be found by running: 

        docker run --rm openapitools/openapi-generator-cli config-help -g {language}
3) If appropriate generate a template (mustache) files to customise the generated output. It is currently necessary to turn off client-side-validation. 
The default templates are available here: https://github.com/OpenAPITools/openapi-generator/tree/master/modules/openapi-generator/src/main/resources
4) Run the above docker run command using the your new config files, and replacing ruby references with {language}
5) The generate directory will contain a README that will contain instructions on how to use the generated library. 
 
For more info see the help docs by running the following:

        docker run --rm openapitools/openapi-generator-cli help

For details usage of this tool as well as other ways the generated clients can be customised, see the official repo: https://github.com/OpenAPITools/openapi-generator