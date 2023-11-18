<template>
  <div class="grid">
      <div class="col-12 md:col-12">
          <div class="card p-fluid">
              <h5>Consumir API REST Empleado</h5>
              <div class="field">
                  <label for="nom">Nombre(S):</label>
                  <InputText id="nom" type="text" />
              </div>
              <div class="field">
                  <label for="salario">Salario:</label>
                  <InputText id="salario" type="text" />
              </div>   
              <div class="field">
                  <label for="edad">Edad:</label>
                  <InputText id="edad" type="text" />
              </div>
              <div class="field">
                  <label for="idem">Id Emp:</label>
                  <InputText id="idem" type="text" />
              </div>
              <div class="col-12 md:col-6">
                  <Button label="Consultar datos" class="p-button-success mr-2 mb-2" icon="pi pi-search" href="employee_name"/>
              </div>
          </div>
          
          <div>
              <h3>Empleados</h3>
              <DataTable v-bind="value" :value="empleados" showGridlines paginator :rows="5"
                  paginatorTemplate="FirstPageLink PrevPageLink PageLinks NextPageLink LastPageLink CurrentPageReport RowsPerPageDropdown"
                  :rowsPerPageOptions="[5, 10, 15, 20, 25]" tableStyle="min-width: 50rem"
                  currentPageReportTemplate="Visualizando {last} de {totalRecords} empleados!">
                  
                  <Column field="employee_name" :sortable="true" header="Nombre"></Column>
                  <Column field="employee_salary" header="Salario"></Column>
                  <Column field="employee_age" header="Edad"></Column>
              </DataTable>
          </div>

      </div>
  </div>
</template>

<script>
  import axios from 'axios';
  export default{
    data(){
      return{ empleados: null}
    },
    mounted(){ 
      this.getEmpleados();
    },
    methods:{
      getEmpleados(){
        axios.get('https://dummy.restapiexample.com/api/v1/employees').then(
          response =>(
            this.empleados = response.data.data
          )
        );
      },
      formatCurrency(value) {
        return "$" + value.toFixed(2);
      }
    }
  }
</script>
