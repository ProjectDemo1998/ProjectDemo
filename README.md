
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;

namespace YourNamespace.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class CustomersController : ControllerBase
    {
        private readonly YourDbContext _context;

        public CustomersController(YourDbContext context)
        {
            _context = context;
        }

        // GET: api/Customers
        [HttpGet]
        public async Task<ActionResult<IEnumerable<Customer>>> GetCustomers()
        {
            return await _context.Customers.ToListAsync();
        }

        // GET: api/Customers/5
        [HttpGet("{id}")]
        public async Task<ActionResult<Customer>> GetCustomer(int id)
        {
            var customer = await _context.Customers.FindAsync(id);

            if (customer == null)
            {
                return NotFound();
            }

            return customer;
        }

        // PUT: api/Customers/5
        [HttpPut("{id}")]
        public async Task<IActionResult> PutCustomer(int id, Customer customer)
        {
            if (id != customer.Id)
            {
                return BadRequest();
            }

            _context.Entry(customer).State = EntityState.Modified;

            try
            {
                await _context.SaveChangesAsync();
            }
            catch (DbUpdateConcurrencyException)
            {
                if (!CustomerExists(id))
                {
                    return NotFound();
                }
                else
                {
                    throw;
                }
            }

            return NoContent();
        }

        // POST: api/Customers
        [HttpPost]
        public async Task<ActionResult<Customer>> PostCustomer(Customer customer)
        {
            _context.Customers.Add(customer);
            await _context.SaveChangesAsync();

            return CreatedAtAction(nameof(GetCustomer), new { id = customer.Id }, customer);
        }

        // DELETE: api/Customers/5
        [HttpDelete("{id}")]
        public async Task<IActionResult> DeleteCustomer(int id)
        {
            var customer = await _context.Customers.FindAsync(id);
            if (customer == null)
            {
                return NotFound();
            }

            _context.Customers.Remove(customer);
            await _context.SaveChangesAsync();

            return NoContent();
        }

        private bool CustomerExists(int id)
        {
            return _context.Customers.Any(e => e.Id == id);
        }
    }
}
This project contains a simple RESTful API for managing customer entities. It supports CRUD (Create, Read, Update, Delete) operations using HTTP verbs (POST, GET, PUT, DELETE).

## Endpoints

### GET /api/customer
Retrieve a list of all customers.

### GET /api/customer/{id}
Retrieve details of a specific customer by ID.

### POST /api/customer
Create a new customer.

### PUT /api/customer/{id}
Update details of an existing customer by ID.

### DELETE /api/customer/{id}
Delete an existing customer by ID.

## Usage

1. Clone this repository.
2. Build and run the project.
3. Use a tool like Postman or cURL to interact with the API endpoints.

## Error Handling

The API returns appropriate HTTP status codes for different scenarios:

- 200 OK: Successful GET request.
- 201 Created: Successful POST request.
- 204 No Content: Successful PUT or DELETE request.
- 400 Bad Request: Malformed request or missing parameters.
- 404 Not Found: Resource not found
