# cardealership_project

# dealershipquery

-- Query that adding customers

CREATE OR REPLACE FUNCTION add_customer( _first_name VARCHAR, _last_name VARCHAR)
RETURNS void 
AS $MAIN$
BEGIN
	INSERT INTO customer(first_name,last_name)
	VALUES( _first_name, _last_name);
END;
$MAIN$
LANGUAGE plpgsql;
SELECT add_customer(3, 'Jamar', 'Jack');
SELECT add_customer(4, 'Bob', 'Marley');
SELECT add_customer(5, 'Will', 'Smith');
SELECT add_customer(6, 'Mike', 'Jordan');
SELECT add_customer(7, 'Mike', 'Jackson');
SELECT add_customer(8, 'Carmelo', 'Anthony');
SELECT add_customer(9, 'Cole', 'Anthony');
SELECT add_customer(10, 'Paul', 'Walker');
Select *
From customer;

-- Query adding time date etc to service ticket

INSERT INTO service_ticket(
		service_ticket_id,
		vin_number,
		part_number,
		service_date,
		part_cost,
		labor_cost,
		total_cost_service,
		mechanic_id
) VALUES(
		1,
		1,
		1,
		CURRENT_DATE,
		50.00,
		75.00,
		125.00,
		1
);

INSERT INTO service_ticket(
		vin_number,
		part_number,
		service_date,
		labor_cost,
		total_cost_service,
		mechanic_id
) 
VALUES(
		2,
		2,
		CURRENT_DATE,
		100.00,
		150.00,
	    250.00,
);
Select *
From service_ticket 
-- Query that add mechanic
CREATE OR REPLACE FUNCTION add_mechanic( _first_name VARCHAR, _last_name VARCHAR)
RETURNS void 
AS $MAIN$
BEGIN
	INSERT INTO mechanic(first_name,last_name)
	VALUES( _first_name, _last_name);
END;
$MAIN$
LANGUAGE plpgsql;
SELECT add_mechanic('Billy', 'Countryman');
SELECT add_mechanic('Nicole', 'Countryman');
SELECT add_mechanic('Devon', 'Mitchell');
SELECT add_mechanic('Ethan', 'Smith');
SELECT add_mechanic('Richard', 'Bowman');
Select *
From mechanic;

CREATE OR REPLACE FUNCTION add_salesperson( _first_name VARCHAR, _last_name VARCHAR)
RETURNS void 
AS $MAIN$
BEGIN
	INSERT INTO salesperson(first_name,last_name)
	VALUES( _first_name, _last_name);
END;
$MAIN$
LANGUAGE plpgsql;
SELECT add_salesperson( 'Jason', 'Walker');
SELECT add_salesperson( 'Richalin', 'Rodney');
SELECT add_salesperson( 'Damion', 'Smith');
SELECT add_salesperson( 'Jordan', 'Wilson');
SELECT add_salesperson( 'Mike', 'Jackson');
SELECT add_salesperson( 'Lemelo', 'Anthony');
SELECT add_salesperson( 'Anthony', 'Cole');
SELECT add_salesperson( 'Dean', 'Walker');
Select *
From salesperson;


INSERT INTO car(
		salesperson_id,
		customer_id,
		car_price
)VALUES (
		4,
		1,
		75000.00
);

INSERT INTO car(
		salesperson_id,
		customer_id,
		car_price
)VALUES (
		3,
		2,
		55000.00
);
Select *
From car;

# dealership table

CREATE TABLE "customer" (
  "customer_id" SERIAL,
  "first_name" VARCHAR(100),
  "last_name" VARCHAR(100),
  PRIMARY KEY ("customer_id")
);

CREATE TABLE "service history" (
  "service_history_id" SERIAL,
  "mechanic_id" INTEGER,
  "vin_number" INTEGER,
  "service_ticket_id" INTEGER,
  PRIMARY KEY ("service_history_id")
);

CREATE TABLE "invoice" (
  "invoice_id" SERIAL,
  "customer_id" INTEGER,
  "salesperson_id" INTEGER,
  "invoice_date" DATE,
  "car_price" NUMERIC(8,2),
  "invoice_total_cost" NUMERIC(8,2),
  "total_cost_service" NUMERIC(8,2),
  PRIMARY KEY ("invoice_id")
);

CREATE TABLE "parts_inventory" (
  "part_number" SERIAL,
  "part_cost" NUMERIC(6,2),
  "part_name" VARCHAR(100),
  PRIMARY KEY ("part_number")
);

CREATE TABLE "service_ticket" (
  "service_ticket_id" SERIAL,
  "vin_number" INTEGER,
  "part_number" INTEGER,
  "service_date" DATE,
  "part_cost" NUMERIC(8,2),
  "labor_cost" NUMERIC(8,2),
  "total_cost_service" NUMERIC(8,2),
  "mechanic_id" INTEGER,
  PRIMARY KEY ("service_ticket_id")
);

CREATE TABLE "salesperson" (
  "salesperson_id" SERIAL,
  "first_name" VARCHAR(100),
  "last_name" VARCHAR(100),
  PRIMARY KEY ("salesperson_id")
);

CREATE TABLE "car" (
  "vin_number" SERIAL,
  "salesperson_id" INTEGER,
  "invoice_id" INTEGER,
  "customer_id" INTEGER,
  "car_price" NUMERIC(8,2),
  PRIMARY KEY ("vin_number")
);

CREATE TABLE "mechanic" (
  "mechanic_id" SERIAL,
  "first_name" VARCHAR(100),
  "last_name" VARCHAR(100),
  PRIMARY KEY ("mechanic_id")
);

