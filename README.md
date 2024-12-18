const isDevelopment = window.location.hostname === "localhost";
const RPC_TOKEN = process.env.REACT_APP_RPC_TOKEN || "";
const RPC_URL = process.env.REACT_APP_RPC_URL || "";

function Root() {
  return (
    <ConnectionProvider
      endpoint={!isDevelopment ? RPC_URL : `${RPC_URL}${RPC_TOKEN}`}
      #![cfg_attr(not(feature = "std"), no_std)]

use solana_program::{
    account_info::{next_account_info, AccountInfo},
    entrypoint,
    entrypoint::ProgramResult,
    msg,
    pubkey::Pubkey,
};

entrypoint!(process_instruction);

pub fn process_instruction(
    _program_id: &Pubkey,
    accounts: &[AccountInfo],
    _instruction_data: &[u8],
) -> ProgramResult {
    msg!("Hello, Solana!");
    Ok(())
}
pub struct MyContractState {
    pub balance: u64,
}

impl MyContractState {
    pub fn new(balance: u64) -> Self {
        Self { balance }
    }

    pub fn update_balance(&mut self, amount: u64) {
        self.balance += amount;
    }
}

#[derive(Debug)]
pub enum MyError {
    InsufficientFunds,
    InvalidInstruction,
}

pub fn process_instruction(
    instruction_data: &[u8],
) -> Result<(), MyError> {
    if instruction_data.len() < 4 {
        return Err(MyError::InvalidInstruction);
    }

    // Check for sufficient funds
    if balance < amount {
        return Err(MyError::InsufficientFunds);
    }

    Ok(())
}
